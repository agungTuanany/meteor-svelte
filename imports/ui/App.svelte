<!-- Implement Svelte Component -->
<script>
    import { Meteor }        from "meteor/meteor"
    import { useTracker }    from "meteor/rdb:svelte-meteor-data";
    import { BlazeTemplate } from "meteor/svelte:blaze-integration"
    import { Issues }        from "../api/issues.js"
    import Issue             from "./Issue.svelte"

    // Reactive Svelte component
    $: issues      = useTracker(() => Issues.find({}).fetch())
    $: currentUser = useTracker(() => Meteor.user())

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
        priority    : newIssue.priority,
        userId      : Meteor.userId(),
        userName    : Meteor.user().username
    })

    newIssue = {
        title       : "",
        description : "",
        dueDate     : "",
        priority    : "low"
    }
}


</script>

<style>
    .head_title {
        margin-top: 110px;
    }

    /* .form_issues { */
    /*     padding-top: 75px; */
    /* } */
</style>


<div>
    <header>
        <nav>
            <a href="#" class="brand">Meteor & Svelte Issue App</a>
            <div class="menu">
                <BlazeTemplate template="loginButtons" data={{align: 'right'}} />
            </div>
        </nav>

        <h1 class="head_title">Issues:</h1>

        {#if $currentUser}
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
        {/if}

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
                    <th></th>
                </tr>
        {#each $issues as issue}
                <Issue issue={issue}/>
        {/each}
            </table>
    </div>
</div>
