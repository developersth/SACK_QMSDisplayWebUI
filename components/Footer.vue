<template>
    <div>
        <v-footer :absolute="fixed" app>
            <v-col class="text-center" cols="12">
                {{ new Date().getFullYear() }} — <strong>G-innovation &copy; </strong>
            </v-col>
        </v-footer>
    </div>
</template>

<script>
export default {
    data() {
        return {
            fixed: false,
        }
    },
}
</script>
  
<style></style>
  