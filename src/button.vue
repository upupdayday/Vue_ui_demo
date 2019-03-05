<template>
    <button class="g-button" :class="{[`icon-${iconPosition}`]: true}"
        @click="$emit('click')"><!--this.$emit('click'),组件内部所以不用this-->
        <g-icon v-if="icon && !loading" :name="icon" class="icon"></g-icon>
        <g-icon v-if="loading" name="loading" class="loading icon"></g-icon>
        <div class="content">
            <slot></slot>
        </div>
    </button>
</template>

<script>
    import Icon from './icon'

    export default {
        components: {
            'g-icon':Icon
        },
        name: 'gButton',
        props: {
            icon: {},
            loading:{
                type: Boolean,
                default: false,
            },
            iconPosition:{
                type: String,
                default: 'left',
                validator: function(value){
                    return ((value === 'left') || (value === 'right'));
                }
            },
        }
    }
</script>

<style lang="scss" scoped>
    /**/
    @keyframes spin
    {
        0% {transform:rotate(0deg);}
        100% {transform:rotate(360deg);}
    }
    .g-button {
        font-size: var(--font-size);
        height: var(--button-height);
        padding: 0 1em;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        display: inline-flex; justify-content: center; align-items: center;
        vertical-align: middle;
        >.content{order: 2;}
        >.icon{order:1; margin-right: .3em;}
        >.loading{animation: spin 2s infinite linear}
        &:hover {
            border-color: var(--border-color-hover);
        }

        &:active {
            background-color: var(--button-active-bg);
        }

        &:focus {
            outline: none;
        }

        &.icon-right{
            >.content{order: 1;}
            >.icon{order: 2; margin-right: 0; margin-left: .3em;}
        }
    }

</style>