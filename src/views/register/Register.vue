<template>
  <div class="wrapper">
    <img class="wrapper_img" src="http://www.dell-lee.com/imgs/vue3/user.png">
    <div class="wrapper_input">
      <input 
        type="text" 
        class="wrapper_input_content" 
        placeholder="请输入用户名"
        v-model="username"
      />
    </div>
    <div class="wrapper_input">
      <input 
        type="password" 
        class="wrapper_input_content" 
        placeholder="请输入密码"
        autocomplete="new-password"
        v-model="password"
      />
    </div>
    <div class="wrapper_input">
      <input 
        type="password" 
        class="wrapper_input_content" 
        placeholder="确认密码"
        v-model="ensurement"
      />
    </div>
    <div class="wrapper_register-button" @click="handleRegister">注册</div>
    <div class="wrapper_register-link" @click="handleLoginClick">已有账号去登录</div>
    <Toast v-if="show" :message="toastMessage"/>  
  </div> 
</template>

<script>
import { useRouter } from 'vue-router';
import { reactive,toRefs } from 'vue'
import { post } from '../../utils/request'
import Toast,{useToastEffect} from '../../components/Toast.vue'

// 注册
const useRegisterEffect=(showToast)=>{
  // useRouter方法获取到路由实例
  const router=useRouter()
  const data = reactive({
    username:'',
    password:'',
    ensurement:''
  })   
  const handleRegister=async()=>{
    try{
      const result=await post('/api/user/register',{
        username:data.username,
        password:data.password
      })
      console.log(result)
      if(result.errno===0){
        router.push({name:'Login'})
      }else{
        showToast('注册失败')
      }
    }
    catch(e){
      showToast('请求失败')
    }      
  }
  const {username,password,ensurement}=toRefs(data)
  // 想当于令username=data.username,password=data.password
  return{username,password,ensurement,handleRegister}
}

// 跳转登录页面
const useLoginEffect=()=>{
  // useRouter方法获取到全局路由实例
  const router=useRouter()
  const handleLoginClick=()=>{
    router.push({name:'Login'})
  }
  return{handleLoginClick}
}

export default {
    name:'Register',
    components:{
      Toast
    },
    setup(){
      const { show,toastMessage,showToast }=useToastEffect()
      const {username,password,ensurement,handleRegister} =useRegisterEffect(showToast)
      const {handleLoginClick} = useLoginEffect()
      return{username,password,ensurement,handleRegister,handleLoginClick,show,toastMessage}
    }
}
</script>

<style lang="scss" scoped>
@import '../../style/virables.scss';
.wrapper{
  position: absolute;
  top: 50%;
  left: 0; 
  right: 0;
  transform: translateY(-50%);
  &_img{
    display: block;
    margin: 0 auto .4rem auto;
    width: .66rem;
    height: .66rem;
  }
  &_input{
    box-sizing: border-box;
    height: .48rem;
    margin: 0 .4rem .16rem .4rem;
    padding: 0 .16rem;
    background: #F9F9F9;
    border: .01rem solid rgb(0, 0, 0,0.10);
    border-radius: .06rem;
    &_content{
        margin-top: .12rem;
        line-height: .22rem;
        border:none;
        outline: none;
        width: 100%;
        background: none;
        font-size: .16rem;
        color: $content-notice-fontColor;
        &::placeholder{
            color: $content-notice-fontColor;
        }
    }
  }
  &_register-button{
    margin: .32rem .4rem .16rem .4rem;
    line-height: .48rem;
    background: $btn-bgColor;
    box-shadow: 0 .04rem .08rem 0 rgba(0,145,225,0.32);
    border-radius: .04rem;
    border-radius: .04rem;
    color: $bgColor;
    font-size: .16rem;
    text-align: center;
  }
  &_register-link{
    font-size: .14rem;
    color: $content-notice-fontColor;
    text-align: center;

  }
}
</style>