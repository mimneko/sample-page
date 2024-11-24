---
title: リンク集
---

- [情報通信ネットワーク](情報通信ネットワーク/test1.md)
- [道徳](道徳/test.md)
- [幾何学](幾何学/test1.md)
- [代数学1](代数学/test1-1.md)
- [代数学2](代数学/test1-2.md)
- [代数学3](代数学/test1-3.md)
- [代数学4](代数学/test1-4.md)
- [代数学5](代数学/test1-5.md)
- [ダウンロード](ダウンロード/)

<div class="folder-tree">
  <ul id="file-list"></ul>
</div>

<script>
const owner = 'mimneko';
const repo = 'sample-page';
const branch = 'main';

async function getFiles(path = '') {
    const url = `https://api.github.com/repos/${owner}/${repo}/contents/${path}?ref=${branch}`;
    const response = await fetch(url);
    const data = await response.json();
    return data;
}

function createFileLink(file) {
    const a = document.createElement('a');
    a.href = `https://${owner}.github.io/${repo}/${file.path}`;
    a.textContent = file.name;
    a.target = '_blank';
    return a;
}

function createFileLink(file) {
    const a = document.createElement('a');
    if (file.name.endsWith('.md')) {
        // .mdファイルは.html形式に変換してリンク
        const htmlName = file.name.replace(/\.md$/, '.html');
        a.href = `https://${owner}.github.io/${repo}/${file.path.replace(file.name, htmlName)}`;
    } else if (file.name.endsWith('.html')) {
        // それ以外は通常のリンク
        a.href = `https://${owner}.github.io/${repo}/${file.path}`;
    }
    a.textContent = file.name;
    a.target = '_blank';
    return a;
}

async function displayFiles(parentElement, path = '') {
    const files = await getFiles(path);
    for (const file of files) {
        if (['README.md', 'index.html', 'script.js', '_config.yml'].includes(file.name)) {
            continue;
        }
        const li = document.createElement('li');
        if (file.type === 'file') {
            li.appendChild(createFileLink(file));
        } else if (file.type === 'dir') {
            const details = document.createElement('details');
            details.open = true; // デフォルトで開いた状態にする
            const summary = document.createElement('summary');
            summary.textContent = file.name;
            details.appendChild(summary);
            const ul = document.createElement('ul');
            details.appendChild(ul);
            li.appendChild(details);
            await displayFiles(ul, file.path);
        }
        parentElement.appendChild(li);
    }
}

displayFiles(document.getElementById('file-list')).catch(console.error);

</script>
