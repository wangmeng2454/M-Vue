<template>
  <el-container style="min-height: 100vh">
    <el-aside :width="sideWidth + 'px'" style="box-shadow: 2px 0 5px #b3c0d1">
      <el-menu :default-openeds="['1', '3']" style="min-height: 100%;width: 200px; overflow-x: hidden;"
               background-color="#b3c0d1" active-text-color="#ffffff" :collapse-transition="false"
               :collapse="isCollapse">
        <div style="height: 60px; line-height: 60px;">
          <img src="../assets/logo.png" style="width: 20px; position: relative; top: 5px; margin-left: 22px" alt="">
          <b style="color: rgb(0, 0, 0);margin-left: 5px;" v-show="logoTextShow">后台管理系统</b>
        </div>
        <el-submenu index="1">
          <template v-slot:title>
            <i class="el-icon-message"></i>
            <span slot="title">导航一</span></template>
          <el-menu-item-group>
            <template v-slot:title>分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="1-4">
            <template v-slot:title>选项4</template>
            <el-menu-item index="1-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="2">
          <template v-slot:title><i class="el-icon-menu"></i><span slot="title">导航二</span></template>
          <el-menu-item-group>
            <template v-slot:title>分组一</template>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="2-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="2-4">
            <template v-slot:title>选项4</template>
            <el-menu-item index="2-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="3">
          <template v-slot:title><i class="el-icon-setting"></i><span slot="title">导航三</span></template>
          <el-menu-item-group>
            <template v-slot:title>分组一</template>
            <el-menu-item index="3-1">选项1</el-menu-item>
            <el-menu-item index="3-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="3-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="3-4">
            <template v-slot:title>选项4</template>
            <el-menu-item index="3-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container>
      <el-header style="font-size: 20px;border-bottom: 1px; line-height: 60px; display: flex" class="el-header">
        <div style="flex:1;width: 60px;margin-left: 20px;">
          <span :class="collapseBtnClass" style="cursor: pointer;" @click="collapse"></span>
        </div>
        <el-dropdown style="margin-right: 10px;cursor: pointer; font-size: 20px;">
          <i class="el-icon-setting" style="margin-left: 10px;"></i>
          <el-dropdown-menu v-slot="dropdown">
            <el-dropdown-item>个人信息</el-dropdown-item>
            <el-dropdown-item>退出</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <span style="margin-right: 10px;">王小明</span>
      </el-header>

      <el-main>
        <div style="margin: 10px 0;">
          <el-input style="width: 300px;" placeholder="数据连接中......检测到输入名称......"
                    suffix-icon="el-icon-user" class="ml-5"></el-input>
          <el-input style="width: 300px; margin-top: 5px" placeholder="数据连接中......检测到输入邮箱......"
                    suffix-icon="el-icon-message" class="ml-5"></el-input>
          <el-input style="width: 300px; margin-top: 5px" placeholder="数据连接中......检测到输入地址......"
                    suffix-icon="el-icon-map-location" class="ml-5"></el-input>
          <el-button style="width: 100px;" class="m-5005" type="primary">搜索</el-button>
        </div>

        <div style="margin: 10px 0">
          <el-button type="primary" style="width: 100px;" class="ml-5">新增<i class="el-icon-circle-plus-outline"></i>
          </el-button>
          <el-button type="danger" style="width: 100px;margin: 5px 0 0 5px">批量删除<i
              class="el-icon-remove-outline"></i></el-button>
          <el-button type="primary" style="width: 100px;margin: 5px 0 0 5px">导入<i
              class="el-icon-bottom"></i></el-button>
          <el-button type="primary" style="width: 100px;margin: 5px 0 0 5px">导出<i class="el-icon-top"></i>
          </el-button>
        </div>

        <el-table :data="tableData" border stripe header-row-class-name="tableHeader" class="tableHeader">
          <el-table-column prop="date" label="日期" width="120">
          </el-table-column>
          <el-table-column prop="name" label="姓名" width="120">
          </el-table-column>
          <el-table-column prop="address" label="地址"></el-table-column>
          <el-table-column label="操作" width="200" align="center">
            <template v-slot:default="scope">
              <el-button type="success">编辑 <i class="el-icon-edit"></i></el-button>
              <el-button type="danger">删除 <i class="el-icon-remove-outline"></i></el-button>
            </template>
          </el-table-column>
        </el-table>

        <div style="padding: 10px;">
          <div class="block">
            <el-pagination :page-sizes="[10, 30, 50, 100]" :page-size="10"
                           layout="total, sizes, prev, pager, next, jumper" :total="100">
            </el-pagination>
          </div>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<style>
.el-header {
  background-color: #b3c0d1;
  color: #333;
  line-height: 60px;
}

.tableHeader, th {
  background-color: #b3c0d1 !important;
}
</style>

<script>
export default {
  data() {
    const item = {
      date: "2021-6-20",
      name: "王小明",
      address: "安徽省芜湖市起飞路",
    };
    return {
      tableData: Array(10).fill(item),
      collapseBtnClass: 'el-icon-s-fold',
      isCollapse: false,
      sideWidth: 200,
      logoTextShow: true
    };
  },
  methods: {
    collapse() { // 点击收缩菜单栏
      this.isCollapse = !this.isCollapse
      if (this.isCollapse) { // 收缩
        this.sideWidth = 60;
        this.collapseBtnClass = 'el-icon-s-unfold';
        this.logoTextShow = false;
      } else { // 展开
        this.sideWidth = 200;
        this.collapseBtnClass = 'el-icon-s-fold';
        this.logoTextShow = true;
      }
    }
  }
};
</script>
