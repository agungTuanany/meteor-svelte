<script>
    /*
    export let title
    export let description
    export let dueDate
    export let priority
    */
    import { Issues } from "../api/issues.js"
    export let issue

function deleteIssue() {
    Issues.remove(issue._id)
}
</script>

<!--
<li>{title}</li>
<li>{description}</li>
<li>{dueDate}</li>
<li>{priority}</li>
-->

<tr>
    <td>{issue.title}       </td>
    <td>{issue.description} </td>
    <td>{issue.dueDate}     </td>
    <td>{issue.priority}    </td>
    <td> <button class="error" on:click={deleteIssue}>Delete</button></td>
</tr>
