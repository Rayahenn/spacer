<template>
    <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
        <p class="subclaim">Begin your journey bla bla bla bla 
            bla bla bla bla bla bla bla bla 
        </p>
        <p class="subclaim">
            Type anything
        </p>
    </div>
</template>

<script>
export default {
    name: "Claim",
}
</script>

<style lang="scss" scoped>
    .claimWrapper {
        display: flex;
        text-align: center;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    
    .claim {
        font-size: 50px;
        margin: 0;
    }

    .subclaim {
        margin-top: 25px;
        font-size: 13px;
    }
</style>