<template>
    <div>
        <el-row :gutter="20">
            <el-col :span="16">
                <el-form ref="form" :model="form" label-width="120px">
                    <el-form-item label="Question">
                        <el-input v-model="form.text" type="textarea" :rows="10"></el-input>
                    </el-form-item>
                    <el-form-item label="Answer Variants">
                        <br>
                        <div>
                            <Answer
                                    v-for="variant in form.variants"
                                    :key="variant.id"
                                    :id="variant.id"
                                    v-on:change-variant="changeVariant"
                            />
                        </div>
                    </el-form-item>
                    <el-form-item label="Tags">
                        <el-select
                                v-model="form.tags"
                                multiple
                                filterable
                                allow-create
                                default-first-option
                                placeholder="Choose tags"
                                class="tags-select"
                        >
                            <el-option
                                    v-for="item in tagsOptions"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="Hint">
                        <el-input v-model="form.hint" type="textarea" :rows="3"></el-input>
                    </el-form-item>
                    <el-form-item label="Hint Url">
                        <el-input v-model="form.hintUrl" ></el-input>
                    </el-form-item>
                </el-form>
            </el-col>
            <el-col :span="8">
                <el-divider>JSON</el-divider>
                <div class="code">
                    <pre id="code_json">{{question}}</pre>
                </div>
                <el-divider>Actions</el-divider>
                <el-button type="success" icon="el-icon-copy-document" round class="btn" :data-clipboard-text="questionJson" >Copy JSON to clipboard</el-button>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    import tagsOptions from '../data/tags';
    import Answer from './MakerAnswer'
    import ClipboardJS from 'clipboard'

    export default {
        name: "MakerForm",
        data() {
            return {
                form: {
                    text: '',
                    tags: [],
                    hint: '',
                    hintUrl: '',
                    variants: [
                        {
                            id: "A",
                            text: "",
                            isCorrect: false
                        },
                        {
                            id: "B",
                            text: "",
                            isCorrect: false
                        },
                        {
                            id: "C",
                            text: "",
                            isCorrect: false
                        },
                        {
                            id: "D",
                            text: "",
                            isCorrect: false
                        }
                    ],
                },
                tagsOptions: tagsOptions
            }
        },
        computed: {
            question: function () {
                return {
                    id: null,
                    text: this.form.text.split(/\r?\n/).join('\n'),
                    answers: [],
                    variants: this.form.variants.map(function (item) {
                        item.text = item.text.split(/\r?\n/).join('\n');

                        return item;
                    }),
                    tags: this.form.tags,
                    hint: this.form.hint.split(/\r?\n/).join('\n'),
                    hintUrl: this.form.hintUrl
                }
            },
            questionJson: function () {
                return this.question && document.getElementById('code_json') ? document.getElementById('code_json').innerText : '';
            }
        },
        methods: {
            changeVariant(id, text, isCorrect) {
                this.form.variants = this.form.variants.map(function (oldItem) {
                    if (oldItem.id === id) {
                        return {
                            id: id,
                            text: text,
                            isCorrect: isCorrect
                        };
                    }
                    return oldItem;
                })
            }
        },
        components: {
            Answer
        },
        mounted: function() {
            var clipboard = new ClipboardJS('.btn');
        }
    }
</script>

<style scoped>
    .tags-select {
        width: 100%;
    }
    .code {
        border-radius: 5px;
        border: 1px solid #DCDFE6;
        background: #f5f5f5;
        overflow: auto;
        padding: 10px 15px;
    }
</style>