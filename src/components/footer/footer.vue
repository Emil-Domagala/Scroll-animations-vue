<template>
    <footer>
        <p><a href="https://twitter.com/logicalhq" target="_blank">@Logicalhq</a></p>
        <p>Copyright © 2023 Logical Software, Inc.</p>
    </footer>
</template>

<style scoped lang='scss'>
@import '../../assets/_colors.css';

footer {

    position: relative;
    left: 0;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 40px;
    padding: 20px 80px;
    font-size: 14px;
    color: #989D9D;

    p {
        display: block;
        margin-block-start: 1em;
        margin-block-end: 1em;
        margin-inline-start: 0px;
        margin-inline-end: 0px;
    }

    a {
        color: var(--black-color);
        text-decoration: none;
    }
}

@media (min-width:1200px) {
    footer {
        position: absolute;
        margin-top: -120px;
        align-items: flex-start;
    }
}
</style>