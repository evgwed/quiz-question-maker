<template>
    <div>
        <el-row :gutter="20">
            <el-col :span="16">
                <el-form ref="makerForm" :model="form" :rules="rules" label-width="120px">
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

                        <el-row :gutter="20">
                            <el-col :span="6">
                                <span :class="['theme-text symfony', (this.showLaravelTags ? '':'active')]">Symfony</span>
                                <el-switch
                                        v-model="showLaravelTags"
                                        active-color="#ff2d20"
                                        inactive-color="#000">
                                </el-switch>
                                <span :class="['theme-text laravel', (this.showLaravelTags ? 'active':'')]">Laravel</span>
                            </el-col>
                            <el-col :span="16">
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
                                            v-for="item in optionsTags"
                                            :key="item.value"
                                            :label="item.label"
                                            :value="item.value">
                                    </el-option>
                                </el-select>
                            </el-col>
                        </el-row>
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
                <el-button type="success" icon="el-icon-copy-document" class="btn" round @click="submitForm('makerForm')" >Copy JSON to clipboard</el-button>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    import tagsOptionsLaravel from '../data/tags_laravel';
    import tagsOptionsSymfony from '../data/tags_symfony';
    import Answer from './MakerAnswer'

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
                rules: {
                    text: [
                        { required: true, message: 'Please input Activity name', trigger: 'blur' },
                        { min: 3, max: 5, message: 'Length should be 3 to 5', trigger: 'blur' }
                    ],
                    tags: [
                        { type: 'array', required: true}
                    ],
                    hint: [
                        { required: true, message: 'Please input Activity name', trigger: 'blur' },
                        { min: 1, max: 5, message: 'Length should be 3 to 5', trigger: 'blur' }
                    ]
                },
                tagsOptions: tagsOptionsLaravel,
                showLaravelTags: true,
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
            optionsTags: function () {
                return this.showLaravelTags ? tagsOptionsLaravel : tagsOptionsSymfony;
            }
        },
        methods: {
            changeVariant(id, text, isCorrect) {
                let form = this.form;
                form.variants = form.variants.map(function (oldItem) {
                    if (oldItem.id === id) {
                        return {
                            id: id,
                            text: text,
                            isCorrect: isCorrect
                        };
                    }
                    return oldItem;
                });
                this.form = form;
            },
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        this.$clipboard(document.getElementById('code_json').innerText);
                        this.$message({
                            message: 'Данные успешно скопированы в буфер обмена.',
                            type: 'success'
                        });
                    } else {
                        this.$message({
                            message: 'Fail copy.',
                            type: 'error'
                        });
                        return false;
                    }
                });
            }
        },
        components: {
            Answer
        },
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
    .theme-text {
        display: inline-block;
        color: #aaa;
    }
    .theme-text.laravel{
        padding-left: 10px;
        width: 60px;
    }
    .theme-text.laravel.active{
        font-weight: bold;
        color: #ff2d20;
    }
    .theme-text.symfony{
        padding-right: 10px;
        width: 60px;
    }
    .theme-text.symfony.active{
        font-weight: bold;
        color: #000;
    }
</style>