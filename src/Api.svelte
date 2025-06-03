<script>
    import ky from 'ky';
    import { each } from 'svelte/internal';

    let posts = []
    var id = 1

    function getPost() {
        // (async () => {
        //     try {
        //     const response = await ky.post('https://jsonplaceholder.typicode.com/posts/1', {
        //         json: { foo: true }
        //     });
        //         const content = await response.json();
        //         console.log(content);
        //     } catch (error) {
        //         console.error('Ошибка запроса:', error);
        //     }
        // })();
        fetch(`https://jsonplaceholder.typicode.com/posts/${id}`)
        .then((response) => response.json())
        .then((json) => {
            console.log(json);
            posts = [...posts, json];
        });
        id++;
    }
    function delPost() {
        fetch(`https://jsonplaceholder.typicode.com/posts/1`, {
            method: 'DELETE',
        });
    }
</script>

<main>
    <div>
        <h1>hello API</h1>
        <button on:click={getPost}>GET</button>
        <button on:click={delPost}>DEL</button>
    </div>
    {#each posts as post, i}
        <div>
            <number>{post.id}</number>
            <div>
                <h2>{post.title}</h2>
                <p>{post.body}</p>
            </div>
            <button on:click={() => posts = posts.toSpliced(i, 1)}>Удалить</button>
        </div>
    {/each}
</main>