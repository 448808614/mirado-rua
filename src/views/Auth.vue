<template>
	<div class="body">
		<a-row type="flex" justify="center" align="top" :bordered="false" class="center">
			<a-col :xs="24" :sm="20" :md="12" :lg="8" :xl="6">
				<a-card title="验证 MIRAODO-RUA" style="width: 100%">
					<a-space direction="vertical" size="middle">
						<InputAccount  placeholder="用户名" v-model:value="username" />
						<InputPassword  placeholder="密码" v-model:value="password" />
						<a-button type="primary" @click="auth" :loading="checking"> 确定 </a-button>
					</a-space>
				</a-card>
			</a-col>
		</a-row>
	</div>
	<a-layout-footer class="footer">
		MIRAIDO - RUA ©2020
	</a-layout-footer>
</template>
<script>
	import {
		UserOutlined,
		KeyOutlined
	} from '@ant-design/icons-vue'

	
	import InputAccount from '@/components/inputs/InputAccount.vue'
	import InputPassword from '@/components/inputs/InputPassword.vue'
	
	export default {
		name: "Auth",
		data() {
			return {
				username: "",
				password: "",
				checking: false
			}
		},
		methods: {
			auth() {
				this.checking = true
				api.post('/auth', {
					username: this.username,
					password: this.password
				}).then(response => {
					this.$message.success('验证通过', 2)
					this.$router.replace("/")
					this.checking = false
				}).catch(response => {
					this.$error({
						title: '验证失败',
						content: '用户名或密码错误！',
					})
					this.checking = false
				})
			}
		},
		components: {
			InputAccount,
			InputPassword,
			UserOutlined,
			KeyOutlined
		},
	};
</script>

<style>
	.center {
		/* vertical-align:middle;
		display:inline-block */
		margin-top: 10%;
	}

	.body {
		background: #ECECEC;
		padding: 30px;
		height: 90%;
	}

	.footer {
		background: #ECECEC;
		height: 10%;
		textAlign: 'center';
	}
</style>
