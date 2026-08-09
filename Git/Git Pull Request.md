### Pull Request

A **Pull Request (PR)** is a request to merge changes from one branch into another, usually from a feature branch into `main`. It allows other developers to **review the changes, discuss them, and approve them** before they are merged. A PR is commonly created on platforms such as GitHub or GitLab.

Typical workflow:

<pre class="overflow-visible! px-0!" data-start="462" data-end="555"><div class="relative w-full mt-4 mb-1"><div class=""><div class="contents"><div class="relative"><div class="h-full min-h-0 min-w-0"><div class="h-full min-h-0 min-w-0"><div class="border border-token-border-light border-radius-3xl corner-superellipse/1.1 rounded-3xl"><div class="h-full w-full border-radius-3xl bg-(--code-block-surface) corner-superellipse/1.1 overflow-clip rounded-3xl [--code-block-surface:var(--bg-elevated-secondary)] dark:[--code-block-surface:var(--composer-surface-primary)] lxnfua_clipPathFallback"><div class="pointer-events-none absolute end-1.5 top-1 z-2 md:end-2 md:top-1"></div><div class="relative"><div class="pe-11 pt-3"><div class="relative z-0 flex max-w-full"><div id="code-block-viewer" dir="ltr" class="q9tKkq_viewer cm-editor z-10 light:cm-light dark:cm-light flex h-full w-full flex-col items-stretch ͼs ͼ16"><div class="cm-scroller"><pre class="cm-content q9tKkq_readonly m-0"><code><span>Create branch → Make changes → Commit → Push → Open Pull Request → Review → Merge</span></code></pre></div></div></div></div></div></div></div></div></div><div class=""><div class=""></div></div></div></div></div></div></pre>

Example:

<pre class="overflow-visible! px-0!" data-start="567" data-end="683"><div class="relative w-full mt-4 mb-1"><div class=""><div class="contents"><div class="border border-token-border-light border-radius-3xl corner-superellipse/1.1 rounded-3xl"><div class="relative h-full w-full border-radius-3xl bg-(--code-block-surface) corner-superellipse/1.1 overflow-clip rounded-3xl [--code-block-surface:var(--bg-elevated-secondary)] dark:[--code-block-surface:var(--composer-surface-primary)] lxnfua_clipPathFallback"><div class="pointer-events-none absolute inset-x-4 top-12 bottom-4"><div class="pointer-events-none sticky z-40 shrink-0 z-1!"><div class="sticky bg-token-border-light"></div></div></div><div class="relative"><div class="h-full min-h-0 min-w-0"><div class="h-full min-h-0 min-w-0"><div class=""><div class="relative"><div class=""><div class="relative z-0 flex max-w-full"><div id="code-block-viewer" dir="ltr" class="q9tKkq_viewer cm-editor z-10 light:cm-light dark:cm-light flex h-full w-full flex-col items-stretch ͼs ͼ16"><div class="cm-scroller"><pre class="cm-content q9tKkq_readonly m-0"><code><span class="ͼ10">git</span><span> switch </span><span class="ͼ12">-c</span><span> feature/login
</span><span class="ͼ10">git</span><span> add .
</span><span class="ͼ10">git</span><span> commit </span><span class="ͼ12">-m</span><span> </span><span class="ͼz">"Add login feature"</span><span>
</span><span class="ͼ10">git</span><span> push </span><span class="ͼ12">-u</span><span> origin feature/login</span></code></pre></div></div></div></div></div></div></div></div><div class=""><div class=""></div></div></div></div></div></div></div></div></pre>

After pushing the branch, you open a **Pull Request** from `feature/login` → `main`.

**Important:** A Pull Request is **not a Git command**. It is a workflow provided by platforms such as GitHub, GitLab, and Bitbucket.
