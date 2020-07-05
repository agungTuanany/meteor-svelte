<script>
    import { Issues } from "../api/issues.js"
    export let issue

    function deleteIssue() {
        Issues.remove(issue._id)
    }
</script>


<tr>
    <td>{issue.title}       </td>
    <td>{issue.description} </td>
    <td>{issue.dueDate}     </td>
    <td>{issue.priority}    </td>
    <td> <button class="error" on:click={deleteIssue}>Delete</button></td>
</tr>
