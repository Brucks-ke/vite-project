<template>
  <el-row :gutter="20">
    <el-col :span="3">

    </el-col>
    <el-col :span="18">
      <el-tabs v-model="activeName" class="demo-tabs">
        <el-tab-pane label="文章列表" name="first">
          <content-list :articleList="articleList"></content-list>
        </el-tab-pane>
        <el-tab-pane label="问题列表" name="second">
          <content-list :articleList="questionList"></content-list>
        </el-tab-pane>
        <el-tab-pane label="笔记列表" name="third">
          <content-list :articleList="bookList"></content-list>
        </el-tab-pane>
        <el-button type="primary" size="small" @click="showDialog" style="float:right;margin-top: 10px;">新增</el-button>
      </el-tabs>
    </el-col>
    <el-col :span="3">
    </el-col>
  </el-row>
  <!-- 对话框 -->
  <el-dialog v-model="dialogStatus" title="新增文章" width="50%" center>
    <!-- 对话框弹窗 -->
    <template #footer>
      <span class="dialog-footer">
        <!-- 对话框显示内容 -->
        <span>
          <el-form ref="ruleFormRef"  label-width="70px" class="demo-ruleForm"
            status-icon>
            <el-form-item label="文章标题" prop="name">
              <el-input v-model="articleInfo.name" />
            </el-form-item>
            <el-form-item label="文章内容" prop="desc">
              <el-input type="textarea" v-model="articleInfo.content" />
            </el-form-item>
          </el-form>
        </span>
        <!-- 对话框显示内容 -->
        <el-button @click="dialogStatus = false">取消</el-button>
        <el-button type="primary" @click="addArticle">
          确定
        </el-button>
      </span>
    </template>
  </el-dialog>

</template>

<script>
import { reactive, ref } from 'vue'
// 导入组件contentList
import contentList from './components/contentList.vue/'
export default {
  components:{
    contentList,
  },
  setup() {
    const activeName = ref('first')
    // 定义文章信息
    const articleInfo = reactive({
      name: "",
      content: "",
    })
    const articleList = reactive([])
    const questionList = reactive([])
    const bookList = reactive([])
    function addArticle() {
      if (activeName.value == "first") {
        articleList.push({ ...articleInfo })        
      }
      else if(activeName.value == "second"){
        questionList.push({ ...articleInfo }) 
      }
      else if(activeName.value == "third"){
        bookList.push({ ...articleInfo }) 
      }
      dialogStatus.value = false
    }
    const dialogStatus = ref(false)
    function showDialog() {
      dialogStatus.value = true
    }
    // 选择了哪一个table

    return {
      activeName,
      articleList,
      addArticle,
      dialogStatus,
      showDialog,
      articleInfo,
      questionList,
      bookList,

    }
  },
}

</script>
<style>
.demo-tabs>.el-tabs__content {
  padding: 32px;
  color: #6b778c;
  font-size: 32px;
  font-weight: 600;
  text-align: center;
}
</style>
