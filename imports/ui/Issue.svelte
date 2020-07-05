<script>
    import { Meteor } from "meteor/meteor"
    import { useTracker } from "meteor/rdb:svelte-meteor-data"
    import { Issues } from "../api/issues.js"

    export let issue

    // Reactive Svelte component
    $: currentUser = useTracker(() => Meteor.user())

    function deleteIssue() {
        Issues.remove(issue._id)
    }
</script>


<tr>
    <td>{issue.title}       </td>
    <td>{issue.description} </td>
    <td>{issue.dueDate}     </td>
    <td>{issue.priority}    </td>
    <td>{issue.userName}    </td>
    {#if $currentUser}
        <td> <button class="error" on:click={deleteIssue}>Delete</button></td>
    {/if}
</tr>
