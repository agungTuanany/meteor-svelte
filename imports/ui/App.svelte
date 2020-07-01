//Implement Svelte componet

<script>
    import Issue from './Issue.svelte'

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
</script>


<div>
    <header>
        <h1>
            Issues:
        </h1>
    </header>
    <ul>
        {#each getIssues() as issue}
            <Issue
                title={issue.title}
                />
        {/each}
    </ul>
</div>
