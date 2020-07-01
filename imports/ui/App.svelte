<!-- Implement Svelte Component -->
<script>
    import { useTracker } from 'meteor/rdb:svelte-meteor-data';
    import { Issues } from "../api/issues.js"
    import Issue from './Issue.svelte'

    // Reactive Svelte component
    $: issues = useTracker(() => Issues.find({}).fetch())

    let newIssue = {
        title       : "",
        description : "",
        dueDate     : "",
        priority    : "low"

    }
/*
function getIssues() {
    return [
        // Dummy object
        { title         : "First Title",
            description : "First Issue Description",
            dueDate     : "2021-02-12",
            priority    : "low"
        },
        { title         : "Second Title",
            description : "Second Issue Description",
            dueDate     : "2021-02-12",
            priority    : "normal"
        },
        { title         : 'Third Title',
            description : "Third Issue Description",
            dueDate     : "2021-02-12",
            priority    : "High"
        },
    ]
}
 */

function handleSubmit(event) {
    Issues.insert({
        title       : newIssue.title,
        description : newIssue.description,
        dueDate     : newIssue.dueDate,
        priority    : newIssue.priority
    })

    newIssue = {
        title       : "",
        description : "",
        dueDate     : "",
        priority    : "low"
    }
}


</script>


<div>
    <header>
        <h1>Issues:</h1>
        <form on:submit|preventDefault={handleSubmit}>
            <label for="title">Title</label>
            <input id="title" type="text" bind:value={newIssue.title}/>
            <label for="description">Description:</label>
            <input id="title" type="text" bind:value={newIssue.description}/>
            <label for="dueDate">Due Date</label>
            <input id="title" type="text" bind:value={newIssue.dueDate}/>
            <label for="priority">Priority:</label>
            <select id="title" type="text" bind:value={newIssue.priority}>
                <option value="low">Low</option>
                <option value="medium">Medium</option>
                <option value="high">High</option>
            </select>
            <input type="submit"/>
        </form>
    </header>
    <div>
            <!--
                <ul>
                <Issue title={ issue.title }
                description={ issue.description }
                dueDate={ issue.dueDate }
                priority={ issue.priority }
                />
                </ul>
            -->
            <table>
                <tr>
                    <th>Title</th>
                    <th>Description</th>
                    <th>Due Date</th>
                    <th>Priority</th>
                </tr>
        {#each $issues as issue}
                <Issue issue={issue}/>
        {/each}
            </table>
    </div>
</div>
