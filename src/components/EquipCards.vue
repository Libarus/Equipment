<template>
    <div>
        <EquipCard v-for="card of cards" :card="card"/>
    </div>
</template>

<script>
    import EquipCard from '@/components/EquipCard';

    export default {
        name: "EquipCards",
        props: {
            cards: {
                required: true
            }
        },
        components: {
            EquipCard
        }
    }
</script>

<style scoped>

</style>
