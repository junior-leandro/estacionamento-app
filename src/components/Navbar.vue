<template>
    <div id="nav">

    <RouterLink to="/" id="logo_url">
        <img :src="logo" :alt="alt" id="logo">
    </RouterLink>
    
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/Cadastro">Cadastro</RouterLink>
    </div>
</template>

<script>

export default{
    name: "Navbar",
    props: ["logo", "alt"]  // Logo e imagens
}

</script>

<style scoped> /* O Style com 'scoped' altera somente o componente em que está */

#nav{
    background-color: #141414;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}
#nav #logo_url{
    margin: auto;
    margin-left: 0;

}

#logo{
    width: 40px;
    height: 40px;
}

#nav a{
    color: #FFFFFF;
    text-decoration: none;
    font-weight: 600;
    margin: 12px;
    transition: .5s;
    font-size: 24px;
}

#nav a:hover{
    color: red;
}
</style>