<script lang="ts">
  import Highlight from '$lib/components/Highlight.svelte';
  import type { PageData } from './$types';

  export let data: PageData;
</script>

<h2>Recipes and caveats</h2>

<h3>Custom HTTP headers</h3>

<p>
  The <code>createTRPCClient</code> method optionally accepts a <code>headers</code> option, which
  can be useful, for example, to set an <code>Authorization</code> header.
</p>

<h3>Using custom data transformers</h3>

<p>
  The <code>createTRPCClient</code> method optionally accepts a <code>transformer</code> option.
  Please refer to
  <a href="https://trpc.io/docs/data-transformers" target="_blank" rel="noreferrer"
    >this section in the tRPC.io documentation</a
  >
  for more information, and keep in mind that you'll have to use the same <code>transformer</code> when
  you're defining the router and when you're creating the client.
</p>
<h3>Response caching</h3>

<p>
  Your server responses must <a
    href="https://vercel.com/docs/concepts/functions/serverless-functions/edge-caching"
    target="_blank"
    rel="noreferrer">satisfy some criteria</a
  >
  in order for them to be cached (i.e. by Vercel's Edge Network). Please refer to
  <a href="https://trpc.io/docs/caching" target="_blank" rel="noreferrer"
    >this section of the tRPC.io documentation</a
  > for more information.
</p>
<p>
  The <code>createHTTPHandle</code> method conveniently alloys you to specify a
  <code>responseMeta</code> function.
</p>

<h3>Inferring types</h3>

<p>
  It is often useful to wrap functionality of your tRPC client API within other functions. For this
  purpose, it's necessary to be able to infer input types and output types generated by your tRPC
  router. The<code>@trpc/server</code> package exports two helper types to assist with inferring
  these types from your router, namely <code>inferRouterInputs</code> and
  <code>inferRouterOutputs</code>. Please refer to
  <a href="https://trpc.io/docs/infer-types" target="_blank" rel="noreferrer"
    >this section of the tRPC.io documentation</a
  >
  for more information.
</p>

<p>
  To make your code faster to type and easier to read, you could further refine these helper types
  when defining your router:
</p>

<Highlight {...data.codeBlocks['bookstall/src/lib/trpc/router.ts']} />

<p>Then, you could use the helper types in your pages code like so:</p>

<Highlight {...data.codeBlocks['bookstall/src/routes/authors/+page.svelte']} />
