<template>
    <fade>
        <div class="overlay is-overlay"
            :class="{ 'is-opaque': !transparent }"
            v-if="visible">
            <div :class="['loader', `is-${size}`]"
                :style="borderColor"/>
        </div>
    </fade>
</template>

<script>
import { Fade } from '@liberu-ui/transitions';

export default {
    name: 'Loader',

    components: { Fade },

    props: {
        color: {
            type: String,
            default: '#f44336',
        },
        size: {
            type: String,
            default: 'medium',
            validator: v => ['small', 'medium', 'large'].includes(v),
        },
        transparent: {
            type: Boolean,
            default: false,
        },
    },

    data: () => ({
        visible: false,
    }),

    computed: {
        borderColor() {
            return {
                'border-color': `${this.color}`,
            };
        },
    },

    mounted() {
        this.visible = true;
    },
};
</script>

<style lang="scss">
    .overlay.is-overlay {
        display: flex;
        border-radius: inherit;

        .loader {
            margin: auto;
            -webkit-animation: spinAround 500ms infinite linear;
            animation: spinAround 500ms infinite linear;
            border-radius: 50%;
            content: "";

            &.is-small {
                height: 1em;
                width: 1em;
                border-width: 0 0 2px 2px;
            }

            &.is-medium {
                width: 2em;
                height: 2em;
                border-width: 0 0 3px 3px;
            }

            &.is-large {
                width: 3em;
                height: 3em;
                border-width: 0 0 4px 4px;
            }
        }

        &.is-opaque {
            background: rgba(255, 255, 255, 0.2);
        }
    }
</style>
