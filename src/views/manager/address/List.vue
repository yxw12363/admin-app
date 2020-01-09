<template>
        <briup-fulllayout title="常用地址">
        <!-- {{address}}
        {{info}} -->
        <van-list >
         <van-cell v-for="item in addresses"
           :key="item.id"
           :title="item.province + ' '+item.city+item.area+item.address"/>
        </van-list>  
        <br>
        <van-button block type="default" @click="toAddressEditHandler">添加</van-button>

        </briup-fulllayout>     
    
</template>

<script>
import {get} from '../../../http/axios';
import { mapState } from 'vuex';
export default {
        data(){
                return{
                        addresses:[]
                }
        },
        created(){
                this.loadAddress();
        },
        computed:{//计算属性
        //状态机中的user对象中的info对象获取到
                ...mapState('user',['info'])
        },
        methods:{
                //加载当前顾客地址信息
                loadAddress(){
                        let id = this.info.id;   //假装当前id为26
                        let url = "/address/findByCustomerId?id="+id;
                        get(url).then((response)=>{
                                this.addresses= response.data;
                        })
                },toAddressEditHandler(){
                        this.$router.push("/manager/address_edit");
                }
                
        }
    
}
</script>
<style scoped>

</style>
