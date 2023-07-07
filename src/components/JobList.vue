<template>
    <div class="job-list">
        <TransitionGroup name="list" tag="ul">
            <li
                v-for="job in orderedJobs"
                :key="job.id"
            >
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <p>
                        {{ job.salary }} rupees
                    </p>
                </div>
                <div class="description">
                    <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Delectus saepe incidunt adipisci veniam! Ex, architecto totam dolore voluptatem, unde facilis, perspiciatis optio dignissimos dolores eaque vitae. Voluptates consequuntur iste aliquam.</p>
                </div>
            </li>
        </TransitionGroup>
    </div>
</template>

<script lang="ts" setup>
import { defineProps, PropType, computed } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";

    const props = defineProps({
        jobs: {
            required: true,
            type: Array as PropType<Job[]>,
        },
        order: {
            required: true,
            type: String as PropType<OrderTerm>,
        }
    });

    const orderedJobs = computed(() => {
        if (props.order === "salary") {
            return [...props.jobs].sort((a: Job, b: Job) => {
                return a[props.order] - b[props.order];
            });
        } else {
            return [...props.jobs].sort((a: Job, b: Job) => {
                return a[props.order].localeCompare(b[props.order]);
            });
        }
    })
</script>

<style scoped>
    .job-list {
        max-width: 960px;
        margin: 40px auto;
    }

    .job-list ul {
        padding: 0;
    }

    .job-list li {
        list-style: none;
        background: #fff;
        padding: 16px;
        margin: 16px 0;
        border-radius: 4px;
    }

    .job-list h2 {
        margin: 0 0 10px;
        text-transform: capitalize;
    }

    .salary {
        display: flex;
    }

    .salary img {
        width: 30px;
    }

    .salary p {
        color: #17bf66;
        font-weight: bold;
        margin: 10px 4px;
    }

    .list-move {
        transition: all .5s;
    }
</style>