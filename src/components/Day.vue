<template>

    <div class="colonne__wrapper">

        <div class="colonne" :style="cssVars"></div>
        <div class="amount">${{amount}}</div>
        <p>{{name}}</p>

    </div>

</template>

<script>
    export default {
        props: {
            name: {
                type: String,
                default: ""
            },
            amount:{
                type: Number,
                default:0
            }
        },
        computed:{
            cssVars(){
                return{
                    '--height':this.amount + 'px',
                }
            }
        }
        
    }
</script>

<style lang="scss" scoped>

    .colonne__wrapper {
        display: flex;
        font-size: 9px;
        flex-direction: column;
        box-sizing: border-box;
        gap: 1rem;
        position: relative;
        align-items: center;
    }
    .colonne{
        max-width: 35px;
        height: calc(var(--height)*2);
        background-color: hsl(10,79%,65%);
        border-radius: .2rem;
        transition: opacity .2s;
        width: 100%;
        &:hover + .amount{
            opacity: 1;
        }
        &:hover{
            opacity: .8;
            cursor: pointer;
        }
    }

    .amount {
        background-color: hsl(25,47%,15%);
        padding: 0.35rem;
        color: white;
        position: absolute;
        font-size: 11px;
        border-radius: 0.2rem;
        top: -2.25rem;
        opacity: 0;
        transition: opacity .2s;
    }

    p {
        font-size: 14px;
        color: hsl(28,10%,53%);
    }

</style>