<template>
    <div class="wrapper" :class="{error: error}">
        <input :value="value" :disabled="disabled" :readonly="readonly" type="text"
           @change="$emit('change', $event.target.value)"
           @input="$emit('input', $event.target.value)"
           @focus="$emit('focus', $event.target.value)"
           @blur="$emit('blur', $event.target.value)">
        <template v-if="error">
            <g-icon name="error" class="icon-error"></g-icon>
            <span class="errorMessage">{{error}}</span>
        </template>
    </div>
</template>

<script>
    export default {
        name: "gInput",
        props: {
            value: {
                type: String
            },
            disabled: {
                type: Boolean,
                default: false
            },
            readonly: {
                type: Boolean,
                default: false
            },
            error:{
                type: String
            }
        }
    }
</script>

<style lang="scss" scoped>
    /*--button-height: 32px;*/
    /*--font-size: 14px;*/
    /*--button-bg: white;*/
    /*--button-active-bg: #eee;*/
    /*--border-radius: 4px;*/
    /*--color: #333;*/
    /*--border-color: #999;*/
    /*--border-color-hover: #666;*/
    $height: 32px;
    $border-color: #999;
    $border-color-hover: #666;
    $border-radius: 4px;
    $font-size: 12px;
    $box-shadow-color: rgba(0, 0, 0, 0.5);
    $red: #F1453D;

    .wrapper {font-size: $font-size; display: inline-flex; align-items: center;
        >:not(:last-child){margin-right: .5em;}
        > input {height: 32px; border: 1px solid $border-color; border-radius: 4px; padding: 0 8px;
            font-size: inherit;
            &:hover {border-color: $border-color-hover;}
            &:focus {box-shadow: inset 0 1px 3px $box-shadow-color; outline: none;}
            &[disabled], &[readonly]{border-color: #bbb; color: #bbb; cursor: not-allowed;}
        }
        &.error{
            >input{border-color: $red;}
        }
        .icon-error{fill: $red; width: 1.2em; height: 1.2em; }
        .errorMessage { color: $red;}
    }

</style>