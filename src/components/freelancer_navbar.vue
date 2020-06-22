<template>
    <nav class="navbar navbar-expand-lg bg-secondary text-uppercase_ fixed-top" id="mainNav">
        <div class="container">
            <rad_logo 
                data="logo" 
                view="horizontal"
                img_size = "50px"
                title_style = "color: white; font-size: 20px; font-family: 'Varela Round', Helvetica, Arial, sans-serif;"
                subtitle_hidden = true
                subtitle_size = "17px"
                desc_size = "11px"/>
            <!-- <a class="navbar-brand js-scroll-trigger" href="#page-top">Start Bootstrap</a> -->
            <button class="navbar-toggler navbar-toggler-right text-uppercase font-weight-bold bg-primary text-white rounded" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
                Menu
                <i class="fas fa-bars"></i>
            </button>
            <div class="collapse navbar-collapse" id="navbarResponsive">
                <rad_menu 
                    data="menu" 
                    ul_class="navbar-nav ml-auto"
                    ul_li_class="nav-item mx-0 mx-lg-1"
                    ul_li_a_class="nav-link py-3 px-0 px-lg-3 rounded js-scroll-trigger"
                    size="25" />
            </div>
        </div>
    </nav>
</template>
<style scoped>
    @import url('https://fonts.googleapis.com/css?family=Varela+Round');
</style>
<script>
   import rad_logo from './rad_logo.vue'
//    import rad_menu from './rad_menu.vue'
  
    export default {
        components: {
            rad_logo//, rad_menu
        }
    }
</script>