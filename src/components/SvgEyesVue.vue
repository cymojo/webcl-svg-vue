<template>
    <div id="eyes">
        <div>
            <Eye id="leftEye"></Eye>
        </div>
        <div>
            <Eye id="rightEye"></Eye>
        </div>
    </div>
</template>

<script>

    import Eye from './Eye.vue'

    export default {
        name: "SvgEyesVue",
        components: {
            Eye
        }

    }
</script>

<style scoped>

    #eyes {
        width:  200px;
        height: 80px;
        position: absolute;
    }
</style>