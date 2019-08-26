<template>
    <div class="variant">
        <el-row :gutter="20">
            <el-col :span="1"><b>{{id}})</b></el-col>
            <el-col :span="17">
                <el-input
                        placeholder="Please input answer"
                        v-model="text"
                        size="small"
                        class="answer_text"
                        @change="change"
                ></el-input>
            </el-col>
            <el-col :span="6">
                <el-radio-group
                        v-model="isCorrect"
                        size="small"
                        @change="change"
                >
                    <el-radio-button :label="true">Correct</el-radio-button>
                    <el-radio-button :label="false">InCorrect</el-radio-button>
                </el-radio-group>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    export default {
        name: "MakerAnswer",
        props: {
            id: String
        },
        data () {
            return {
                text: '',
                isCorrect: false,
            };
        },
        methods: {
            change() {
                this.$emit('change-variant', this.id, this.text, this.isCorrect);
            }
        }
    }
</script>

<style scoped>
    .variant {
        width: 100%;
    }
    .answer_text {
        width: 100%;
    }
</style>