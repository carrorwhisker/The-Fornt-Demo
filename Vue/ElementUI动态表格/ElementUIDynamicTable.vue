<template>
  <div class="add-norms">
    <div style="display: flex">
      <el-button type="text" icon="el-icon-plus"
                 @click="addDomain" style="margin-left: 1%"
                 size="mini">
        添加
      </el-button>
    </div>
    <el-table :data="addForm.properties" border class="normTable">
      <el-table-column label="排序" min-width="2">
        <template slot-scope="scope">
          <el-form-item :prop="'properties.' + scope.$index + '.sequence'"
                        :rules="rules.properties.sequence" label-width="0px">
            <el-input
                style="width:250px"
                v-model.number="scope.row.sequence"
            ></el-input>
          </el-form-item>
        </template>
      </el-table-column>
      <el-table-column label="规格值" min-width="2">
        <template slot-scope="scope">
          <el-form-item :prop="'properties.' + scope.$index + '.value'"
                        :rules="rules.properties.value" label-width="0px">
            <el-input
                style="width:250px"
                v-model="scope.row.value"
            ></el-input>
          </el-form-item>
        </template>
      </el-table-column>
      <el-table-column label="操作" min-width="1">
        <template slot-scope="scope">
          <el-button type="text" icon="el-icon-delete"
                     @click="removeDomain(scope.row)"
                     circle size="mini">
            删除
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      //表单标签宽度
      formLabelWidth: '85px',
      //表格值
      addForm: {
        properties: []
      },
      //验证规则
      rules: {
        name: [required("请输入名称")],
        // sequence: [integerGreaterThanOrEqualToZero("请输入规格序号且为整数")],

        //动态表单验证规则
        properties: [{
          value: [required('请输入规格值')],
          // sequence: [integerGreaterThanOrEqualToZero('请输入排序且为整数')]
        }]
      }
    }
  },
  methods: {
    //新增规格值
    addDomain() {
      this.addForm.properties.push({
        sequence: 0,
        value: ''
      });
      this.rules.properties.push(this.rules.properties[0]);
    },

    //删除规格值
    removeDomain(item) {
      let index = this.addForm.properties.indexOf(item)
      if (index !== -1) {
        this.addForm.properties.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped>

</style>