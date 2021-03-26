<template>
    <h1>Hello</h1>
</template>

<script>
import axios from "axios";
export default {
    middleware: 'isAuthenticated',
}
</script>