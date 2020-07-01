<!-- Implement Svelte Component -->
<script>
    import { useTracker } from 'meteor/rdb:svelte-meteor-data'
    import { Issues } from "../api/issues.js"
    import Issue from './Issue.svelte'

    // Reactive Svelte component
    $: issues = useTracker(() => Issues.find({}).fetch())
/*
function getIssues() {
    return [
        // Dummy object
        { title       : "First Title",
            description : "First Issue Description",
            dueDate     : "2021-02-12",
            priority    : "low"
        },
        { title       : "Second Title",
            description : "Second Issue Description",
            dueDate     : "2021-02-12",
            priority    : "normal"
        },
        { title       : 'Third Title',
            description : "Third Issue Description",
            dueDate     : "2021-02-12",
            priority    : "High"
        },
    ]
}
*/

</script>


<div>
    <header>
        <h1>
            Issues:
        </h1>
    </header>
    {#each $issues as issue}
        <!--
        <ul>
            <Issue title={ issue.title }
                description={ issue.description }
                dueDate={ issue.dueDate }
                priority={ issue.priority }
            />
        </ul>
        -->

        <ul>
            <Issue
                issue={ issue }
            />

        </ul>

    {/each}
</div>
