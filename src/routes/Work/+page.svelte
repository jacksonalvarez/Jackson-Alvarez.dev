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
    .green-title {
        color: var(--green-color); /* Apply the green color */
    }

    .content-section {
        animation: fadeIn 0.8s ease-in-out;
    }

    @keyframes fadeIn {
        0% {
            opacity: 0;
            transform: translateY(10px);
        }
        100% {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .section-item {
        padding: 16px;
        border: 1px solid #ddd;
        background-color: #f5f5f5;
        margin-bottom: 16px;
        border-radius: 8px;
        transition: transform 0.3s ease-in-out;
    }

    .section-item:hover {
        transform: translateY(-5px);
        box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
    }

    .container {
        display: flex;
        flex-direction: column;
        gap: 16px;
    }

    .section-container {
        display: flex;
        flex-direction: column;
        gap: 16px;
    }

    /* Flex layout for side-by-side content inside each section */
    .content-flex {
        display: flex;
        justify-content: space-between;
        gap: 16px;
    }
        .content-flex-noline {
        display: flex;
        justify-content: space-between;
        gap: 60px;
    }

    .content-flex > .left, .content-flex > .right {
        flex: 1;
    }

    /* Adding a vertical line between left and right content */
    .content-flex .left {
        border-right: 2px solid #ddd;
        padding-right: 16px;
    }

    /* Custom Tailwind colors */
    .primary-bg { background-color: #3490dc; } /* Blue */
    .secondary-bg { background-color: #38c172; } /* Green */
    .tertiary-bg { background-color: #f9f9f9; } /* Light Grey */
    .primary-text { color: #3490dc; }
    .secondary-text { color: #38c172; }
    .tertiary-text { color: #6c757d; }
</style>

<div class="container h-full mx-auto flex flex-col items-center">
    <!-- Experience Section -->
<section class="content-section mb-4 text-center">
    <h2 class="text-4xl font-semibold primary-text mb-5">Experience</h2>
    <div class="section-container">
        <div class="card shadow-md bg-tertiary-bg text-tertiary-text border border-base-200 rounded-lg p-6 transition-all hover:shadow-lg hover:bg-base-200">
            <div class="content-flex">
                <div class="left">
                    <h3 class="font-semibold text-xl secondary-text">Student System Admin</h3>
                    <h6 class="bg-tertiary-bg tertiary-text font-medium py-2 rounded-md w-full hover:bg-primary-focus">May 2023 - Current</h6>
                    <p>I am a windows system administrator with two years of experience. I write applications that are used against our site server to facilitate best practices for Windows device compliance and application management. I do this part-time while I attend university.</p>
                </div>
                <div class="right">
                    <h3 class="font-semibold text-xl secondary-text">Digital Integration Intern</h3>
                    <h6 class="bg-tertiary-bg tertiary-text font-medium rounded-md w-full hover:bg-primary-focus">Summer 2022</h6>
                    <p>Created a live product information management system for Hoodsly.com over the summer of 2022. I got to work in office full time for 4 months, helping with CRM management and different technical problems thrown my way.</p>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="content-flex-noline">
<div class="left">
<!-- Technologies Section -->
<section class="content-section mb-4 text-center">
    <h2 class="text-4xl font-semibold primary-text mb-5">Technologies</h2>
    <div class="section-container">
        <div class="card shadow-md bg-tertiary-bg text-tertiary-text border border-base-200 rounded-lg p-6 transition-all hover:shadow-lg hover:bg-base-200">
            <div class="content-flex">
                <div class="left">
                    <h3 class="font-semibold text-xl py-2 secondary-text">Languages:</h3>
                    <p>C++/C#/C, Python, Javascript, Haskell, Java, R</p>
                </div>
                <div class="right">
                    <h3 class="font-semibold text-xl py-2 secondary-text">Operating Systems:</h3>
                    <p>Windows, UNIX systems</p>
                </div>
            </div>
        </div>
    </div>
</section>
</div>
<div class="right">
<!-- Technologies Section -->
<section class="content-section mb-4 text-center">
    <h2 class="text-4xl font-semibold primary-text mb-5">Education</h2>
    <div class="section-container">
        <div class="card shadow-md bg-tertiary-bg text-tertiary-text border border-base-200 rounded-lg p-6 transition-all hover:shadow-lg hover:bg-base-200">
                <div>
                    <h3 class="font-semibold text-xl secondary-text">Appalachian State University</h3>
                    <h6 class="bg-tertiary-bg tertiary-text font-medium py-2 rounded-md w-full hover:bg-primary-focus">Fall 2021 - Current | Grad in July 2025</h6>
                    <p>B.S. in Computer Science with mathmatics concentraion</p>

                </div>
        </div>
    </div>
</section>
</div>
</div>


    <hr class="w-full border-t-4 border-gray-300"/>

    <!-- GitHub Projects Section -->
    <section class="content-section mb-8 text-center">
        <h2 class="text-4xl font-semibold primary-text mb-5">Projects Published on GitHub</h2>

        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-3 xl:grid-cols-3 gap-6">
            {#each $projects as repo}
                <div class="card shadow-md bg-tertiary-bg text-tertiary-text border border-base-200 rounded-lg p-2 transition-all hover:shadow-lg hover:bg-base-200">
                    <div class="card-content">
                        <h2 class="font-semibold text-xl secondary-text py-2">{repo.name}</h2>
                        <p class="py-2">{repo.description || 'No description available.'}</p>
                        <a href="{repo.html_url}" target="_blank" class="btn bg-tertiary-bg tertiary-text font-medium py-2 rounded-md w-full hover:bg-primary-focus">
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
                        borderColor: '#3490dc', // Primary color
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
