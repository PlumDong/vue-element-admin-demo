<template>
  <div>
    <el-table :data="stu">
      <el-table-column label="编号" prop="id"></el-table-column>
      <el-table-column label="姓名" prop="name"></el-table-column>
      <el-table-column label="性别" prop="sex"></el-table-column>
      <el-table-column label="年龄" prop="age"></el-table-column>
      <el-table-column
        fixed="right"
        label="操作"
        width="100"
      >
        <template slot-scope="scope">
          <el-button @click="handleUpdate(scope.row)" type="text" size="smali">修改</el-button>
          <el-button @click="handleDelete(scope.row)" type="text" size="smali">删除</el-button>

        </template>

      </el-table-column>
    </el-table>
    <el-dialog width="22%" :visible.sync="updateVisible">
      <el-form :model="updateForm">
        <el-form-item label="编码" >
          <el-input size="mini" :readonly="true" v-model="updateForm.id"></el-input>
        </el-form-item>

        <el-form-item label="姓名">
          <el-input size="mini" v-model="updateForm.name"></el-input>
        </el-form-item>

        <el-form-item label="性别">
          <el-select size="mini"  v-model="updateForm.sex">
            <el-option value="男">男</el-option>
            <el-option value="女">女</el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="年龄" >
          <el-input size="mini" v-model="updateForm.age"></el-input>
        </el-form-item>
        <el-form-item>

        </el-form-item>
          <el-button type="primary" size="mini" @click="confirmUpdate()">确认</el-button>
      </el-form>

    </el-dialog>
  </div>
</template>


<script>
import {all, del, update, insert} from "@/api/student";


const options = {
  async mounted() {
    const {data} = await all();
    this.stu = data;

  },
  data() {
    return {
      stu: [],
      updateVisible: true,
      updateForm: {
        id: 0,
        name: '',
        sex: '男',
        age: 18
      }
    }
  },
  methods: {
    confirmUpdate(){
      update(this.updateForm.id,this.updateForm)
    },
    handleUpdate(row) {
      this.updateVisible = true
      this.updateForm = {...row}

    },
    async handleDelete({id}) {
      try {
        await this.$confirm("确认删除？", {
          confirmButtonText: '确认',
          cancelButtonText: '取消',
          type: 'warning'
        })
        const {code, message} = await del(id);
        if (code === 20000) {

        }
        console.log(data)
        await this.all()
      } catch (e) {
        console.log("取消删除！", e)
      }

    },
    async all() {
      const {data} = await all()
      this.stu = data
    }
  }
}
export default options;
</script>


<style scoped lang="scss">

</style>
