<script>
import { ref, onMounted, onUnmounted } from 'vue';

export default {
    name: 'Timeline',
    setup() {
        const isCollapsed = ref(false);
        const isMobile = ref(false);

        const timelineItems = ref([
            {
                icon: 'fas fa-pen',
                iconClass: 'bg-success',
                title: '<a href="https://dhammike.com/" target="_blank" rel="noopener noreferrer class="text-primary">Consent form </a> signed',
                time: '09:45 AM'
            },
            {
                icon: 'fas fa-person',
                iconClass: 'bg-info',
                title: '3 treatments chosen',
                description: 'Root canal\nDental extraction\nTeeth whitening',
                time: '09:45 AM'
            },
            {
                icon: 'fas fa-plane',
                iconClass: 'bg-warning',
                title: '<a href="https://dhammike.com/" target="_blank" rel="noopener noreferrer class="text-primary">Bundle2 </a> sent',
                description: 'johnsmith@gmail.com',
                time: '3 July, 16:15 PM'
            },
            {
                icon: 'fas fa-remove',
                iconClass: 'bg-danger',
                title: '<a href="https://dhammike.com/" target="_blank" rel="noopener noreferrer class="text-primary">Consent form </a> decline',
                time: '3 July, 12:54 PM'
            },
            {
                icon: 'fas fa-eye',
                iconClass: 'bg-purple',
                title: '<a href="https://dhammike.com/" target="_blank" rel="noopener noreferrer class="text-primary">Bundle1 </a> view',
                description: 'Emergency form',
                time: '3 July, 12:54 PM AM'
            },

            {
                icon: 'fas fa-plane',
                iconClass: 'bg-white',
                title: '<a href="https://dhammike.com/" target="_blank" rel="noopener noreferrer class="text-primary">Bundle1 </a> sent',
                description: 'Emergency form',
                time: '1 July, 10:05 AM'
            },

        ]);

        const timelineItems2 = ref([

            {
                icon: 'fas fa-section',
                iconClass: 'bg-success',
                title: 'Amelioration added',
                time: '09:45 AM'
            },
            {
                icon: 'fas fa-video',
                iconClass: 'bg-info',
                title: '<a href="https://www.youtube.com/watch?v=CRwpBxsIvuE&ab_channel=DHEntertainment" rel="noopener noreferrer  target="_blank" class="text-primary">Periodontics video </a> played',
                description: 'Video completed',
                time: '09:45 AM'
            },
            {
                icon: 'fas fa-check-circle',
                iconClass: 'bg-white',
                title: 'Periodontics selected',
                time: '09:45 AM'
            },
            {
                icon: 'fas fa-clipboard-check',
                iconClass: 'bg-white',
                title: 'Periodontics mentioned',
                time: '09:45 AM'
            }

        ]);

        const appointmentInfo = ref([
            'Appointment End • 1 July 10:00 AM',
        ]);

        const toggleTimeline = () => {
            if (!isMobile.value) {
                isCollapsed.value = !isCollapsed.value;
            } else {
                isCollapsed.value = !isCollapsed.value;
            }
        };

        const checkScreenSize = () => {
            isMobile.value = window.innerWidth <= 768;
            if (isMobile.value) {
                isCollapsed.value = true;
            }
            isMobile.value = window.innerWidth <= 768;
            if (isMobile.value) {
                isCollapsed.value = false;
            }

        };

        onMounted(() => {
            checkScreenSize();
            window.addEventListener('resize', checkScreenSize);
        });

        onUnmounted(() => {
            window.removeEventListener('resize', checkScreenSize);
        });

        return {
            timelineItems,
            timelineItems2,
            appointmentInfo,
            isCollapsed,
            isMobile,
            toggleTimeline
        };
    }
};
</script>

<template>
    <aside class="timeline-section">
        <div class="timeline-content-wrapper" :class="{ collapsed: isCollapsed }">
            <h3 class="timeline-header" @click="toggleTimeline">
                <span class="toggle-icon" :class="{ collapsed: isCollapsed }">
                    <i class="fas fa-chevron-right"></i>
                    <i class="fas fa-chevron-right"></i>
                </span>
                <span class="timeline-title">Timeline</span>
            </h3>
            <hr class="top-hr">

            <div v-for="(item, index) in timelineItems" :key="index" class="timeline-item">
                <div class="timeline-icon" :class="item.iconClass">
                    <i v-if="item.icon.startsWith('fas')" :class="item.icon"></i>
                    <span v-else>{{ item.icon }}</span>
                </div>
                <div v-if="!isCollapsed" class="timeline-content">
                    <div class="timeline-time">{{ item.time }}</div>
                    <!-- <div class="timeline-sub-title">{{ item.title }}</div> -->
                    <div class="timeline-sub-title" v-html="item.title"></div>
                    <div v-if="item.description" class="timeline-desc">{{ item.description }}</div>

                </div>
            </div>


            <hr class="doted-hr" />

            <h2 class="ap-end-title">Appointment Begins • 1 July, 9:45 AM</h2>

            <div v-for="(item, index) in timelineItems2" :key="index" class="timeline-item">
                <div class="timeline-icon" :class="item.iconClass">
                    <i v-if="item.icon.startsWith('fas')" :class="item.icon"></i>
                    <span v-else>{{ item.icon }}</span>
                </div>
                <div v-if="!isCollapsed" class="timeline-content">
                    <div class="timeline-time">{{ item.time }}</div>
                    <div class="timeline-sub-title" v-html="item.title"></div>
                    <!-- <div class="timeline-sub-title">{{ item.title }}</div> -->
                    <div v-if="item.description" class="timeline-desc">{{ item.description }}</div>

                </div>

                <!--  -->

            </div>

            <div v-if="!isCollapsed" v-for="(info, index) in appointmentInfo" :key="index" class="timeline-appointment">
                {{ info }}
            </div>
        </div>
    </aside>
</template>

<style lang="scss" scoped></style>