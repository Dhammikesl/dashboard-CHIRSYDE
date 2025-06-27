<script>
import { ref, onMounted, onUnmounted } from 'vue'
import { SvgIcons } from './SvgIcons.vue'

export default {
    name: 'Sidebar',
    props: {
        isOpen: {
            type: Boolean,
            default: false
        }
    },
    emits: ['close'],
    setup(props, { emit }) {
        const menuItems = ref([
            { iconComponent: SvgIcons.Home, label: 'Home', active: false },
            { iconComponent: SvgIcons.Sessions, label: 'View sessions >', active: false },
            { iconComponent: SvgIcons.Parent, label: 'Patient records', active: true },
            { iconComponent: SvgIcons.Media, label: 'Media', active: false },
            { iconComponent: SvgIcons.Virtual, label: 'Virtual consultation', active: false },
            { iconComponent: SvgIcons.Statistics, label: 'Statistics', active: false }
        ])

        const setActiveItem = (index) => {
            menuItems.value.forEach((item, i) => {
                item.active = i === index
            })
        }

        const handleOutsideClick = (event) => {
            if (window.innerWidth <= 768 && props.isOpen) {
                const sidebar = document.querySelector('.sidebar')
                const menuBtn = document.querySelector('.mobile-menu-btn')

                if (!sidebar.contains(event.target) && menuBtn && !menuBtn.contains(event.target)) {
                    emit('close')
                }
            }
        }

        onMounted(() => {
            document.addEventListener('click', handleOutsideClick)
        })

        onUnmounted(() => {
            document.removeEventListener('click', handleOutsideClick)
        })

        return {
            menuItems,
            setActiveItem
        }
    }
}
</script>

<template>
    <nav class="sidebar" :class="{ open: isOpen }">
        <div class="sidebar-brand">
            <a href="/" class="navbarlogo w-nav-brand" aria-label="home"><img
                    src="https://cdn.prod.website-files.com/67163c8a1296ee10c03f4ab3/67f4ed5c1cf06beff9b5f819_Logo.webp"
                    loading="lazy" alt="" class="navbarlogoimg"></a>
        </div>
        <div class="sidebar-nav-wrapper">
            <ul class="sidebar-nav">
                <li v-for="(item, index) in menuItems" :key="index" class="sidebar-nav-item">
                    <a @click="setActiveItem(index)" class="sidebar-nav-link" :class="{ active: item.active }">
                        <component v-if="item.iconComponent" :is="item.iconComponent" class="sidebar-icon" />
                        <i v-else :class="item.iconClass" class="sidebar-icon"></i>
                        {{ item.label }}
                    </a>
                </li>
            </ul>
            <ul class="sidebar-nav bottom">
                <div class="sidebar-nav-item">
                    <span class="user">
                        RL
                    </span>
                    <div>
                        <span>Robert Lindley</span>
                        <span class="email">robertlindley@shoreditchdesign.com</span>
                    </div>

                </div>
            </ul>
        </div>
    </nav>
</template>

<style lang="scss" scoped>
.sidebar-icon {
    width: 18px;
    height: 18px;
    margin-right: 10px;
    vertical-align: middle;
}

.navbarlogo {
    justify-content: center;
    align-items: center;
    width: 100%;
    max-width: 143px;
    height: 100%;
    display: flex;

    img {
        max-height: 22px;

    }
}
</style>
