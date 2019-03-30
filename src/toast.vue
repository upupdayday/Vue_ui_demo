<template>
    <div class="toast" @click="onClickClose">
        <slot></slot>
        <div class="line"></div>
        <span class="close" v-if="closeButton">
            {{closeButton.text}}
        </span>
    </div>
</template>

<script>
    export default {
        name: "gToast",
        props:{
            autoClose:{
                type: Boolean,
                default: true
            },
            autoCloaseDelay:{
                type: Number,
                default: 5
            },
            closeButton:{
                type:Object,
                default(){
                    return{
                        text: "关闭",
                        callback: undefined
                    }
                }
            }
        },
        mounted(){
            if(this.autoClose){
                setTimeout(()=>{
                    this.close()
                }, this.autoCloaseDelay*1000)
            }
        },
        methods:{
            close(){
                this.$el.remove()
                this.$destroy()
            },
            onClickClose(){
                this.close();
                if(this.closeButton && typeof this.closeButton.callback === 'function'){
                    this.closeButton.callback(this);
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    $font-size: 14px;
    $toast-height: 40px;
    $toast-bg: rgba(0,0,0,0.75);
    .toast{
        font-size:$font-size; height: $toast-height; line-height: 1.8;
        position: fixed; top:0; left:50%; transform: translateX(-50%);
        display: flex; align-items: center;
        box-shadow: 0 0 3px 0 rgba(0,0,0,0.50);
        border-radius: 4px;
        padding: 0 16px;
        background: $toast-bg;
        color: white;
    }
    .close{
        padding-left: 16px;
    }
    .line{
        height:100%;
        border-left: 1px solid red;
        margin-left: 16px;
    }
</style>