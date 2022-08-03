<template>
    <div>
        <H1>Welcome</H1>
        <p>Hello , welcome to your first Inertia app!</p>
        <Link href="/about">Go to about us</Link>
    </div>
</template>

<script>
import { Link } from "@inertiajs/inertia-vue";
export default {
    components: {
        Link
    },
    name: "Home"
}
</script>

<style scoped>

</style>
