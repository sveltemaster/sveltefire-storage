<script>
    import {UploadTask, StorageRef} from 'sveltefire';
    export let user;
    export let auth;

    let files = '';
    let filename = '';
    $: path = user.email + '/' + filename;
    $: file = files[0];

    let showDownload = false;
    let downloadFilename = '';
    $: downloadPath = user.email + '/' + downloadFilename;
</script>
<h1>You are {user.email}</h1>
<h2>Upload</h2>
{#if file && filename}
    <UploadTask {file} {path} let:task let:snapshot let:downloadURL={url}>

    Uploading your file...

    Progress: {(snapshot.bytesTransferred / snapshot.totalBytes) * 100} %

    <div slot="complete">
        Success! Download here {url}
    </div>

    <div slot="fallback">
        Error or canceled
    </div>

    </UploadTask>
{/if}

<input type="text" bind:value={filename}>
<input type="file" bind:files={files}>
<h2>Download</h2>
{#if showDownload}
    <StorageRef path={downloadPath} let:downloadURL let:ref meta let:metadata> 
    
        <img src={downloadURL} />

        <div slot="loading">
            Loading...
        </div>

        <div slot="fallback">
            Error
        </div>
    </StorageRef>
{/if}
<input type="text" bind:value={downloadFilename}>
<br>
<button on:click={() => showDownload = true} type="submit" class="cursor-pointer bg-gray-700 hover:bg-gray-600 shadow-xl px-5 py-2 inline-block text-blue-100 hover:text-white rounded">Download</button>
<br>
<button on:click={() => auth.signOut()} type="submit" class="cursor-pointer bg-orange-600 hover:bg-orange-500 shadow-xl px-5 py-2 inline-block text-orange-100 hover:text-white rounded">Sign Out</button>