# kb

Code snippet library and brief technical documentation.

<script>
    (async () => {
        const response = await fetch('https://api.github.com/repos/jkmartindale/kb/contents/');
        const data = await response.json();
        document.getElementById('main_content').innerHTML = 
            '<ul>'
            + data
                .filter(file => file.name.endsWith('.md') && file.name != 'README.md')
                .map(file => `<li><a href="${file.name.slice(0, -3)}">${file.name.slice(0, -3)}</a></li>`)
                .join('')
            + '</ul>';
    })()
</script>
