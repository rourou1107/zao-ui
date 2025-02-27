<template>
    <button class="gulu-button" :class="classes" :disabled="disabled">
        <span class="gulu-loadingIndicator" v-if="loading"></span>
        <slot />
    </button>
</template>
<script lang="ts">
    import { computed } from 'vue'
    export default {
        props: {
            theme: {
                type: String,
                default: 'button'
            },
            size: {
                type: String,
                default: 'normal'
            },
            level: {
                type: String,
                default: 'normal'
            },
            disabled: {
                type: Boolean,
                default: false
            },
            loading: {
                type: Boolean,
                default: false
            }
        },
        setup(props) {
          const { theme, size, level } = props
          const classes = computed(() => {
              return {
                  [`gulu-theme-${theme}`]: theme,
                  [`gulu-size-${size}`]: size,
                  [`gulu-level-${level}`]: level,
              }
          })
          return { classes }
        }
    }
</script>
<style lang="scss">
    $h: 32px;
    $border-color: #d9d9d9;
    $color: #333;
    $blue: #40a9ff;
    $red: red;
    $grey: grey;
    $radius: 4px;
    .gulu-button{
        box-sizing: border-box;
        height: $h;
        line-height: $h;
        padding: 0 12px;
        cursor: pointer;
        display: inline-block;
        justify-content: center;
        align-items: center;
        white-space: nowrap;
        background: #ffffff;
        color: $color;
        border: 1px solid $border-color;
        border-radius: $radius;
        box-shadow: 0 1px 0 fade-out(black, 0.95);
        & + & {
            margin-left: 8px;
        }
        &:hover, &:focus {
            color: $blue;
            border-color: $blue;
        }
        &:focus {
            outline: none;
        }
        &::-moz-focus-inner {
            border: 0
        }
        &.gulu-theme-button {
            &.gulu-level-main {
                background: $blue;
                color: #ffffff;
                border-color: $blue;
                &:hover, &:focus {
                    background: darken($blue, 10%);
                    border-color: darken($blue, 10%);
                }
            }
            &.gulu-level-danger {
                background: $red;
                color: #ffffff;
                border-color: $red;
                &:hover, &:focus {
                    background: darken($red, 10%);
                    border-color: darken($red, 10%);
                }
            }
            &[disabled] {
                cursor: not-allowed;
                color: $grey;
                &:hover {
                    border-color: $grey;
                }
            }
        }
        &.gulu-theme-link {
            border-color: transparent;
            box-shadow: none;
            color: $blue;
            &:hover, &:focus {
                color: lighten($blue, 10%);
            }
            &.gulu-level-danger {
                color: $red;
                &:hover, &:focus {
                    color: darken($red, 10%);
                }
            }
        }
        &.gulu-theme-text {
            border-color: transparent;
            box-shadow: none;
            color: inherit;
            &:hover, &:focus {
                background: darken(white, 5%);
            }
            &.gulu-level-danger {
                color: $red;
                &:hover, &:focus {
                    color: darken($red, 10%);
                }
            }
            &.gulu-level-main {
                color: $blue;
                &:hover, &:focus {
                    color: darken($blue, 10%);
                }
            }
        }
        &.gulu-theme-link, &.gulu-theme-text {
            &[disabled] {
                cursor: not-allowed;
                color: $grey;
            }
        }
        &.gulu-size-big {
            font-size: 24px;
            height: 48px;
            line-height: 48px;
            padding: 0 16px;
        }
        &.gulu-size-small {
            font-size: 12px;
            height: 20px;
            line-height: 20px;
            padding: 0 4px;
        }
        > .gulu-loadingIndicator {
            width: 14px;
            height: 14px;
            display: inline-block;
            margin-right: 4px;
            border-radius: 8px;
            border-color: $blue $blue $blue transparent;
            border-width: 2px;
            border-style: solid;
            animation: gulu-spin 1s infinite ;
        }
        @keyframes gulu-spin {
            0%{ transform: rotate(0deg) }
            100%{ transform: rotate(360deg) }
        }
    }
</style>
