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
        color: white;
    }
    
    .claim {
        font-size: 50px;
        margin: 0;

        @media (min-width: 768px) {
            font-size: 80px;
        }
    }

    .subclaim {
        margin: 20px 0 0 0;
        
        margin-top: 25px;
        font-size: 13px;

        @media (min-width: 768px) {
            width: 500px;
            font-size: 17px;
            line-height: 1;
            letter-spacing: 1px;
        }
    }
</style>