<template>
    <div class="demo-collapse">
        <el-collapse v-model="ListName" accordion style="">
            <el-collapse-item v-for="(item, index) in articleList" :key="index" :title="item.name" :name="index">
                <div>
                    {{ item.content }}
                </div>
            </el-collapse-item>

        </el-collapse>
    </div>
</template>

<script>
import { reactive, ref } from 'vue'
export default {
    props: ['articleList'],
    setup(props) {
        // 定义articleList
        const articleList = reactive(props.articleList)
        const ListName = ref('1')
        return {
            articleList,
            ListName
        }
    }
}
</script>