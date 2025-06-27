<script>
import { ref } from 'vue';

export default {
    name: 'Notes',
    setup() {
        const activeTab = ref('notes');
        const lastUpdated = ref('Last updated today 09:15 AM');
        const isEditing = ref(false);

        const noteItems = ref([
            {
                label: 'Dentist',
                content: 'Dr John Smith',
                type: 'text'
            },
            {
                label: 'Nurse',
                content: 'Jane Jones',
                type: 'text'
            },
            {
                label: 'When did the fracture occur?',
                type: 'options',
                options: [
                    { text: 'Today', selected: false },
                    { text: 'Yesterday', selected: false },
                    { text: 'Several days ago', selected: false },
                    { text: 'Over a week ago', selected: true },
                    { text: 'N/A', selected: false }
                ]
            },
            {
                label: 'Location of broken tooth',
                content: 'Broken tooth lorem',
                type: 'text'
            },
            {
                label: 'Reason for attendance',
                content: 'Broken tooth lorem',
                type: 'text'
            },
            {
                label: 'When did the fracture occur?',
                content: 'Broken tooth',
                type: 'text'
            },
            {
                label: 'How did it happen?',
                content: 'Broken tooth',
                type: 'text'
            }
        ]);

        const setActiveTab = (tab) => {
            activeTab.value = tab;
        };

        const selectOption = (itemIndex, optionIndex) => {
            const item = noteItems.value[itemIndex];
            if (item.type === 'options') {
                item.options.forEach((option, index) => {
                    option.selected = index === optionIndex;
                });
            }
        };

        const toggleEdit = () => {
            if (isEditing.value) {
                // Save changes and update timestamp
                const now = new Date();
                const timeStr = now.toLocaleTimeString('en-US', {
                    hour: '2-digit',
                    minute: '2-digit',
                    hour12: true
                });
                lastUpdated.value = `Last updated today ${timeStr}`;
            }
            isEditing.value = !isEditing.value;
        };

        const updateContent = (itemIndex, newContent) => {
            noteItems.value[itemIndex].content = newContent;
        };

        return {
            activeTab,
            lastUpdated,
            noteItems,
            isEditing,
            setActiveTab,
            selectOption,
            toggleEdit,
            updateContent
        };
    }
};
</script>

<template>
    <div class="section-wrapper">
        <section class="tab-section">
            <div class="tabs">
                <button class="tab-btn" :class="{ active: activeTab === 'notes' }" @click="setActiveTab('notes')">
                    <span>Notes</span>
                </button>
                <button class="tab-btn" :class="{ active: activeTab === 'bundles' }" @click="setActiveTab('bundles')">
                    <span>Bundles</span>
                </button>
            </div>
            <div class="d-flex align-items-center justify-content-between">
                <h1>{{ title }}</h1>
                <button class="btn-edit" @click="toggleEdit">
                    <i :class="isEditing ? 'fas fa-save' : 'fas fa-edit'"></i>
                    {{ isEditing ? 'Save session' : 'Edit session' }}
                </button>
            </div>
        </section>
        <section class="notes-section">
            <div v-if="activeTab === 'notes'" class="notes-content">
                <div class="notes-header temp">
                    <div class="notes-template"><span><svg width="24px" height="24px" viewBox="0 0 24 24" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <path fill-rule="evenodd" clip-rule="evenodd"
                                    d="M9.29289 1.29289C9.48043 1.10536 9.73478 1 10 1H18C19.6569 1 21 2.34315 21 4V20C21 21.6569 19.6569 23 18 23H6C4.34315 23 3 21.6569 3 20V8C3 7.73478 3.10536 7.48043 3.29289 7.29289L9.29289 1.29289ZM18 3H11V8C11 8.55228 10.5523 9 10 9H5V20C5 20.5523 5.44772 21 6 21H18C18.5523 21 19 20.5523 19 20V4C19 3.44772 18.5523 3 18 3ZM6.41421 7H9V4.41421L6.41421 7ZM7 13C7 12.4477 7.44772 12 8 12H16C16.5523 12 17 12.4477 17 13C17 13.5523 16.5523 14 16 14H8C7.44772 14 7 13.5523 7 13ZM7 17C7 16.4477 7.44772 16 8 16H16C16.5523 16 17 16.4477 17 17C17 17.5523 16.5523 18 16 18H8C7.44772 18 7 17.5523 7 17Z"
                                    fill="#000000" />
                            </svg></span><span>Template A</span></div>
                    <div class="note-icon">
                        <div class="nt-icon"><svg width="16px" height="16px" viewBox="0 0 24 24" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M6 11C6 8.17157 6 6.75736 6.87868 5.87868C7.75736 5 9.17157 5 12 5H15C17.8284 5 19.2426 5 20.1213 5.87868C21 6.75736 21 8.17157 21 11V16C21 18.8284 21 20.2426 20.1213 21.1213C19.2426 22 17.8284 22 15 22H12C9.17157 22 7.75736 22 6.87868 21.1213C6 20.2426 6 18.8284 6 16V11Z"
                                    stroke="#1C274C" stroke-width="1.5" />
                                <path opacity="0.5"
                                    d="M6 19C4.34315 19 3 17.6569 3 16V10C3 6.22876 3 4.34315 4.17157 3.17157C5.34315 2 7.22876 2 11 2H15C16.6569 2 18 3.34315 18 5"
                                    stroke="#1C274C" stroke-width="1.5" />
                            </svg></div>
                        <div class="nt-icon"><svg width="16px" height="16px" viewBox="0 0 24 24" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M12 6.25C12.4142 6.25 12.75 6.58579 12.75 7V12.1893L14.4697 10.4697C14.7626 10.1768 15.2374 10.1768 15.5303 10.4697C15.8232 10.7626 15.8232 11.2374 15.5303 11.5303L12.5303 14.5303C12.3897 14.671 12.1989 14.75 12 14.75C11.8011 14.75 11.6103 14.671 11.4697 14.5303L8.46967 11.5303C8.17678 11.2374 8.17678 10.7626 8.46967 10.4697C8.76256 10.1768 9.23744 10.1768 9.53033 10.4697L11.25 12.1893V7C11.25 6.58579 11.5858 6.25 12 6.25Z"
                                    fill="#1C274C" />
                                <path
                                    d="M7.25 17C7.25 16.5858 7.58579 16.25 8 16.25H16C16.4142 16.25 16.75 16.5858 16.75 17C16.75 17.4142 16.4142 17.75 16 17.75H8C7.58579 17.75 7.25 17.4142 7.25 17Z"
                                    fill="#1C274C" />
                                <path fill-rule="evenodd" clip-rule="evenodd"
                                    d="M11.9426 1.25C9.63423 1.24999 7.82519 1.24998 6.4137 1.43975C4.96897 1.63399 3.82895 2.03933 2.93414 2.93414C2.03933 3.82895 1.63399 4.96897 1.43975 6.41371C1.24998 7.82519 1.24999 9.63423 1.25 11.9426V12.0574C1.24999 14.3658 1.24998 16.1748 1.43975 17.5863C1.63399 19.031 2.03933 20.1711 2.93414 21.0659C3.82895 21.9607 4.96897 22.366 6.4137 22.5603C7.82519 22.75 9.63423 22.75 11.9426 22.75H12.0574C14.3658 22.75 16.1748 22.75 17.5863 22.5603C19.031 22.366 20.1711 21.9607 21.0659 21.0659C21.9607 20.1711 22.366 19.031 22.5603 17.5863C22.75 16.1748 22.75 14.3658 22.75 12.0574V11.9426C22.75 9.63423 22.75 7.82519 22.5603 6.41371C22.366 4.96897 21.9607 3.82895 21.0659 2.93414C20.1711 2.03933 19.031 1.63399 17.5863 1.43975C16.1748 1.24998 14.3658 1.24999 12.0574 1.25H11.9426ZM3.9948 3.9948C4.56445 3.42514 5.33517 3.09825 6.61358 2.92637C7.91356 2.75159 9.62177 2.75 12 2.75C14.3782 2.75 16.0864 2.75159 17.3864 2.92637C18.6648 3.09825 19.4355 3.42514 20.0052 3.9948C20.5749 4.56445 20.9018 5.33517 21.0736 6.61358C21.2484 7.91356 21.25 9.62178 21.25 12C21.25 14.3782 21.2484 16.0864 21.0736 17.3864C20.9018 18.6648 20.5749 19.4355 20.0052 20.0052C19.4355 20.5749 18.6648 20.9018 17.3864 21.0736C16.0864 21.2484 14.3782 21.25 12 21.25C9.62177 21.25 7.91356 21.2484 6.61358 21.0736C5.33517 20.9018 4.56445 20.5749 3.9948 20.0052C3.42514 19.4355 3.09825 18.6648 2.92637 17.3864C2.75159 16.0864 2.75 14.3782 2.75 12C2.75 9.62178 2.75159 7.91356 2.92637 6.61358C3.09825 5.33517 3.42514 4.56445 3.9948 3.9948Z"
                                    fill="#1C274C" />
                            </svg></div>
                    </div>
                </div>
                <div class="notes-header">
                    <h2 class="notes-title">Notes</h2>
                    <small>{{ lastUpdated }}</small>
                </div>

                <div v-for="(item, itemIndex) in noteItems" :key="itemIndex" class="note-item">
                    <div class="note-label">{{ item.label }}</div>

                    <div v-if="item.type === 'text'" class="note-content">
                        <textarea v-if="isEditing" :value="item.content"
                            @input="updateContent(itemIndex, $event.target.value)" class="note-textarea"
                            rows="2"></textarea>
                        <span v-else>{{ item.content }}</span>
                    </div>

                    <div v-else-if="item.type === 'options'" class="note-options">
                        <div v-for="(option, optionIndex) in item.options" :key="optionIndex" class="note-option"
                            :class="{ selected: option.selected }"
                            @click="isEditing ? selectOption(itemIndex, optionIndex) : null">
                            {{ option.text }}
                        </div>
                    </div>
                </div>
            </div>

            <div v-else-if="activeTab === 'bundles'" class="notes-content">
                <div class="notes-header">
                    <h2 class="notes-title">Bundles</h2>
                    <small>Bundle information will be displayed here</small>
                </div>
                <p>Bundle content goes here...</p>
            </div>
        </section>
    </div>
</template>

<style lang="scss" scoped></style>