<template>
    <el-card shadow="never" :body-style="{ padding: '20px 20px 20px 20px' }">
        <el-tabs>
            <el-tab-pane label="基本设置">
                <el-form ref="form" :model="form" label-width="80px">
                    <el-form-item label="用户名">
                        <el-input></el-input>
                    </el-form-item>
                    <el-form-item label="手机号码">
                        <el-input  class="input-with-select"></el-input>
                    </el-form-item>
                    <el-form-item label="电子邮件">
                        <el-input></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary">更新</el-button>
                    </el-form-item>
                </el-form>
            </el-tab-pane>
            <el-tab-pane label="修改密码">
                <el-form ref="form" :model="form" label-width="80px">
                    <el-form-item label="原密码">
                        <el-input type="password"></el-input>
                    </el-form-item>
                    <el-form-item label="新密码">
                        <el-input type="password"></el-input>
                    </el-form-item>
                    <el-form-item label="确认密码">
                        <el-input type="password"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary">确认修改密码</el-button>
                    </el-form-item>
                </el-form>
            </el-tab-pane>
        </el-tabs>
    </el-card>
</template>
<script>
export default {
  name: "Profile",
  data() {
    return {
      test: true
    };
  },
  mounted() {}
};
</script>
