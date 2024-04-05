<script setup lang="ts">

import { useSlideContext } from '@slidev/client/context.ts'
const { $slidev } = useSlideContext()

console.log($slidev?.nav.tocTree);

</script>

<template>
    <div>
        <h1>test</h1>
    </div>
</template>
