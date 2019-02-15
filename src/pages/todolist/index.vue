<template>
  <div class="todolist">
    <h1 style="text-align: center;margin: 20px 0;">To Do List</h1>
    <el-row :gutter="20">
      <el-col :span="22" :offset="1">
        <son-com v-for="(item, index) in sonComData"
                 :key="index"
                 :tipsName="item.tipsName"
                 :type="item.type"
                 :options="item.options"
                 @changeInput="changeInput"
                 @changeSelect="changeSelect"
                 :inputValueProp="nameValue"
                 :selectValueProp="ageValue">
        </son-com>
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="23">
        <div style="text-align: right; margin-right: 7px;">
          <el-button type="primary" @click="addData">添加</el-button>
          <el-button type="danger" @click="clearValue">重置</el-button>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="22" :offset="1">
        <div class="table-module">
          <el-table
            :data="tableData"
            style="width: 100%">
            <el-table-column
              prop="name"
              label="姓名">
            </el-table-column>
            <el-table-column
              prop="age"
              label="年龄">
            </el-table-column>
            <el-table-column label="操作" width="200">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  type="danger"
                  @click="handleDelete(scope.$index, scope.row)">删除
                </el-button>
              </template>
            </el-table-column>
          </el-table>
        </div>
        <el-row>
          <el-col :span="24">
            <div style="text-align: center; margin-top: 20px;">
              <el-button type="danger" @click="clearAll">删除全部</el-button>
            </div>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import sonCom from '@/components/sonCom.vue'

  export default {
    name: "todolist",
    data() {
      return {
        sonComData: [
          {
            tipsName: '姓名',
          },
          {
            tipsName: '年龄',
            type: 'select',
            options: [
              {
                value: 19,
                label: 19
              },
              {
                value: 20,
                label: 20
              },
              {
                value: 21,
                label: 21
              }
            ]
          }
        ],
        nameValue: '',
        ageValue: '',
        tableData: []
      }
    },
    components: {
      sonCom
    },
    methods: {
      // 组件输入值后暴露出来给父组件中使用
      changeInput(nameValue) {
        // console.log(nameValue)
        this.nameValue = nameValue
      },
      // 组件选择值后暴露出来给父组件中使用
      changeSelect(ageValue) {
        // console.log(ageValue)
        this.ageValue = ageValue
      },
      // 重置
      clearValue() {
        this.nameValue = ''
        this.ageValue = ''
      },
      handleDelete(parm1, parm2) {
        console.log(parm1, '第一个值')
        console.log(parm2, '第二个值')
        this.tableData.splice(parm1, 1)
        this.$message.success('删除成功')
      },
      addData() {
        if (this.nameValue && this.ageValue) {
          let tableDataItem = {
            name: this.nameValue,
            age: this.ageValue
          }
          // 给表格中添加数据
          this.tableData.push(tableDataItem)
          // 恢复默认置空
          this.nameValue = ''
          this.ageValue = ''
        } else {
          this.$message.error('请填写完整信息')
        }
      },
      clearAll() {
        this.tableData = []
        this.$message.success('删除成功')
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>
