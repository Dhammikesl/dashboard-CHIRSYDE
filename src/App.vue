<script>
import { ref } from 'vue';
import Sidebar from './components/Sidebar.vue';
import Header from './components/Header.vue';
import Notes from './components/Notes.vue';
import Timeline from './components/Timeline.vue';
import { library } from '@fortawesome/fontawesome-svg-core'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  name: 'CHAIRSIDE',
  components: {
    Sidebar,
    Header,
    Notes,
    Timeline
  },
  setup() {
    const sidebarOpen = ref(false);

    const breadcrumbs = ref([
      'Patient records',
      'Sarah Thompson',
      'Emergency visit for tooth ache'
    ]);


    const toggleSidebar = () => {
      sidebarOpen.value = !sidebarOpen.value;
    };

    const closeSidebar = () => {
      sidebarOpen.value = false;
    };

    return {
      sidebarOpen,
      breadcrumbs,
      toggleSidebar,
      closeSidebar
    };
  }
};
</script>



<template>
  <div class="container-fluid">
    <div class="row m-0">
      <div class="col p-0">
        <div class="dashboard-layout">
          <Sidebar :isOpen="sidebarOpen" @close="closeSidebar" />

          <main class="main-content">
            <Header :breadcrumbs="breadcrumbs" @toggle-sidebar="toggleSidebar" />

            <div class="content-body">
              <Notes />
            </div>
          </main>
          <Timeline />
        </div>
      </div>
    </div>
  </div>
</template>



<style lang="scss">
@import './styles/global';
</style>