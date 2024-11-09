<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';

    const username = 'jacksonalvarez'; // Replace with your GitHub username
    const token = import.meta.env.VITE_GITHUB_TOKEN; // Replace with your GitHub token if needed

    const projects = writable([]);
    const commitData = writable([]);

    onMount(async () => {
        await fetchGitHubData();
    });

    async function fetchGitHubData() {
        const reposResponse = await fetch(`https://api.github.com/users/${username}/repos`, {
            headers: token ? { Authorization: `token ${token}` } : {}
        });
        const repos = await reposResponse.json();

        const commitsResponse = await fetch(`https://api.github.com/users/${username}/events`, {
            headers: token ? { Authorization: `token ${token}` } : {}
        });
        const commits = await commitsResponse.json();

        projects.set(repos);
        processCommitData(commits);
    }

    function processCommitData(commits) {
        const commitCounts = {};
        
        commits.forEach(commit => {
            const date = new Date(commit.created_at).toDateString();
            commitCounts[date] = (commitCounts[date] || 0) + 1;
        });

        commitData.set(commitCounts);
    }

    // Prepare data for the chart
    let labels = [];
    let data = [];
    commitData.subscribe(commitCounts => {
        labels = Object.keys(commitCounts);
        data = Object.values(commitCounts);
    });
</script>

<style>
    :root {
        --primary-color: #3b82f6;
        --secondary-color: #ef4444;
        --tertiary-color: #3f83f8;
        --green-color: #22c55e; /* Custom green color */
    }

    .green-title {
        color: var(--green-color); /* Apply the green color */
    }
</style>

<div class="container h-full mx-auto flex flex-col items-center">    
    <!-- New Content Section -->
    <section class="content-section mb-8 text-center">
        <h2 class="text-2xl font-semibold text-primary-600 mb-2">About My Work</h2>
        <p class="text-lg max-w-xl mx-auto">
            Update this junk
        </p>
    </section>
    
    <hr class="w-full border-t-2 border-gray-300 my-6" />
        <section class="content-section mb-8 text-center">
        <h2 class="text-2xl font-semibold text-primary-600 mb-2">About My Work</h2>

    <!-- Projects Section -->
    <div class="container grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    {#each $projects as repo}
        <div class="card shadow-md bg-base-100 text-base-content border border-base-200 rounded-lg p-6 transition-all hover:shadow-lg hover:bg-base-200">
            <div class="card-content">
                <h2 class="text-xl font-semibold text-2xl mb-2 green-title">{repo.name}</h2>
                <p class="text-sm text-base-content mb-4">{repo.description || 'No description available.'}</p>
                <a href="{repo.html_url}" target="_blank" class="btn bg-primary text-primary-content font-medium py-2 rounded-md w-full hover:bg-primary-focus">
                    View on GitHub
                </a>
            </div>
        </div>
    {/each}
</div>
</section>


    <!-- Chart Script Section -->
    <script>
        import Chart from 'chart.js/auto';

        // Create the chart
        $: if (labels.length && data.length) {
            const ctx = document.getElementById('commitChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Commits',
                        data: data,
                        borderColor: 'var(--primary-color)',
                        backgroundColor: 'rgba(59, 130, 246, 0.2)',
                        borderWidth: 1,
                    }]
                },
                options: {
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'Date'
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'Number of Commits'
                            }
                        }
                    }
                }
            });
        }
    </script>
</div>
