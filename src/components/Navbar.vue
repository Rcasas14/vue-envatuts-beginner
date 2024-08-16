<template>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid" :class="[`bg-${theme}`]">
            <a class="navbar-brand " href="#" :class="[`text-${textTheme}`]">Navbar</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li v-for="(page, index) in pages" class="nav-item  " :key="index">
                        <navbar-link 
                            :page="page" 
                            :isActive="activePage === index"
                            :class="{[`text-${textTheme}`]: true}" 
                            @click.prevent="navLinkClick(index)">
                        </navbar-link>

                        <!-- <a class="nav-link opacity-75"
                            :class="{active: activePage == index, [`text-${textTheme}`]: true}" aria-current="page"
                            :href="page.link.url" :title="`This link is ${page.link.text}`"
                            @click.prevent="navLinkClick(index)">{{ page.link.text }}</a> -->
                    </li>
                </ul>
                <form class="d-flex justify-content-end">
                    <button class="btn btn-primary" @click.prevent="changeTheme()">Toggle
                        THIS</button>
                </form>
            </div>
        </div>
    </nav>

</template>

<script>
    import NavbarLink from './NavbarLink.vue';
    export default {
        components: {
            NavbarLink,
        },
        props: ['pages', 'activePage', 'navLinkClick'],
        template: `
    `,
        created() {
            this.getThemeSetting();
        },
        data() {
            return {
                theme: 'light',
                textTheme: 'dark',

            }
        },

        methods: {
            changeTheme() {
                let theme = 'light';
                let textTheme = 'dark';

                if (this.theme == 'light') {
                    theme = 'dark';
                }

                if (this.textTheme == 'dark') {
                    textTheme = 'light'
                }

                this.theme = theme;
                this.textTheme = textTheme;
                this.storeThemeSetting();
            },
            storeThemeSetting() {
                localStorage.setItem('theme', this.theme);
                localStorage.setItem('text-theme', this.textTheme);
            },
            getThemeSetting() {
                let theme = localStorage.getItem('theme')
                let textTheme = localStorage.getItem('text-theme')

                if (theme) {
                    this.theme = theme;
                    this.textTheme = textTheme;
                }
            }
        }
    }
</script>