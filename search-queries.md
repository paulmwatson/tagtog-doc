---
layout: page
title: Search queries
sidebar_link: true
id: search_queries

api_document_url: https://www.tagtog.net/-api/documents/v1
api_username: yourUsername
api_pwd: yourPassword
api_project: yourProjectName
toc: true
---

<div class="two-third-col">
  <p>Here you can learn how to build your search queries.</p>
</div>
<div class="one-third-col">
  {% include message.html message='To build more advanced queries you can base on the <a href="http://lucene.apache.org/core/3_1_0/queryparsersyntax.html ">Query Parser Syntax from Lucene</a>' %}
</div>
<div class="two-third-col">
  <h3>Search by string</h3>
  <p>Retrieve documents containing a specific string. Example: <code>insulin</code></p>
</div>
<div class="one-third-col">
  {% include message.html message='Use <code>&ast;</code> as search query to retrieve <strong>all</strong> documents in a project.' %}
</div>

<div class="two-third-col">
  <h3>Search by document label</h3>
  <p>Find documents tagged with specific label and value. </p>
  <p>Boolean example: <code>label:isSevere:true</code></p>
  <p>Enum example: <code>label:severity:high</code></p>
</div>
<div class="one-third-col">

</div>

<div class="two-third-col">
  <h3>Search by entity type</h3>
  <p>Retrieve all documents containing at least one entity that belongs to the given entity type. Example: <code>entity:disease</code>, retrieves all documents with at least one entity of the type <code>disease</code>.</p>
  <p>If you add a term, e.g. <code>entity:disease:cancer</code>, you can find all documents containing at least one entity using that term.</p>
  <br/>
  <p>Only by using the entity type id, you can also perform more advanced queries as:</p>
  <ul>
    <li><code>count</code> e.g. <code>count_e_1:[2 TO &ast;]</code>): retrieve documents with at least 2 annotations of the type <code>e_1</code>.</li>
    <li><code>norms_count_uniq</code> e.g. <code>norms_count_uniq_e_1:[2 TO &ast;]</code> retrieve documents with at least 2 annotations of the type <code>e_1</code> that are normalized to different unique names (e.g Rezulin and Romozin - same diabetic drug sold under different commercial names - would be normalized to troglitazone, so it would count 1 unique entity normalized, not 2).</li>
  </ul>
</div>
<div class="one-third-col">
  {% include message.html message='You can also use the entity type id. E.g. <code>entity:e_1</code>.' %}
</div>


<div class="two-third-col">
  <h3>Search by normalization</h3>
  <p>Retrieve all documents containing at least one entity that normalizes to the given normalization. Example: <code>entity:genes:HER2</code>, retrieves all documents with at least one entity <code>gene</code> that normalizes to <code>HER2</code>.</p>
</div>
<div class="one-third-col">

</div>


<div class="two-third-col">
  <h3>Search by date</h3>
  <p>Retrieve all documents imported or updated in a given time frame.</p>
  <p><code>created</code>: documents imported in a given time frame. Examples: <code>created:2018</code>, <code>created:2018-03</code>, <code>created:2018-03-06</code>, <code>created:[2013 to NOW]</code>, <code>created:[2016-12 TO 2017-02]</code>, <code>created:[NOW-1DAY TO NOW]</code> - documents imported since the previous day.</p>
  <p><code>updated</code>: documents updated in a given time frame. Examples: <code>updated:2018</code>, <code>updated:2018-03</code>, <code>updated:2018-03-06</code>, <code>updated:[2013 to NOW]</code>, <code>updated:[2016-12 TO 2017-02]</code>, <code>updated:[NOW-1DAY TO NOW]</code> - documents updated since the previous day.</p>
</div>
<div class="one-third-col">
</div>


<div class="two-third-col">
  <h3>Search by folder</h3>
  <p>You have three possibilities to search by folder:</p>
  <ol>
    <li><strong>Search by folder index (<code>folder:INDEX</code>)</strong>: the folders' indexes (integer numbers) are written in the <a title="Project settings JSON" href="projects.html#export-settings">project settings JSON</a>. Take note of the folder's index you want to search for, and then search like <code>folder:INDEX</code>. For example, to search for the <code>pool</code> documents (special folder, always created), search like: <code>folder:0</code>.</li>

    <li><strong>Search by folder path (<code>folder:PATH</code>)</strong>: for example, if the structure of your desired folder is <em>pool &gt; level1 &gt; A</em>, compose the folder path as in Unix: <code>folder:pool/level1/A</code>. Note that any leading or trailing <code>/</code>'s are discouraged, although accepted and ignored.</li>

    <li><strong>Search by folder name (<code>folder:NAME</code>)</strong>: following the previous example, you could simply search by <code>folder:A</code>. In case you have different folders with the same name, the folder closest to the root level (the pool), that is, the folder less deep in the folder tree, will be found. For instance, if you had the folders <em>pool/level1/A</em> and <em>pool/level1/level2/A</em>, the former folder will be found. Caveat: in case you have different folders with the same name at the same level of the folder tree, one will be arbitrarily chosen and returned.</li>
  </ol>
</div>
<div class="one-third-col">
  {% include message.html message='<div><p>Searching by folder name is the easiest method. However, if you have different folders with the same name, you should search by folder index or folder path.</p><p>Searching by folder index is the most "robust" method for the indices do not change upon folder renamings.</p></div>' %}
</div>


<div class="two-third-col">
  <h3>Search confirmed documents</h3>
  <p>You can search which documents are confirmed with query: <code>anncomplete:true</code>.</p>
  <p>You can search which documents are not confirmed with query: <code>anncomplete:false</code>.</p>
</div>
<div class="one-third-col">
  {% include message.html message="Here, a <strong>confirmed document</strong> means a document with the master version of the annotations confirmed." %}
</div>

<div class="two-third-col">
  <h3>Search which documents a user has confirmed</h3>
  <p>You can retrieve the documents a given member has confirmed with the query: <code>members_anncomplete:username</code></p>
  <p>You can also retrieve all the documents that have been confirmed by <em>at least one</em> member with the query: <code>members_anncomplete:*</code></p>
  <p>Create a query for a set of users following this example: <code>members_anncomplete:user1 AND members_anncomplete:user2 AND members_anncomplete:user3</code></p>
</div>
<div class="one-third-col">
  {% include message.html message='Find out on this tutorial <a href="https://medium.com/@tagtog/how-to-rank-review-your-annotators-4a814c941ac3?source=friends_link&sk=c354f53823defdaf2844271185fd28e3" title="Medium post: How to rank &amp; review your annotators">how to rank &amp; review your annotators with the <code>members_anncomplete</code> query</a>.' %}
</div>
<div class="one-third-col">
  {% include message.html message='Note that <code>members_anncomplete</code> searches in members versions only. If you rather want to search for a confirmed document in any <em>version</em> (i.e. any member or master), you need to search for: <code>members_anncomplete:* OR anncomplete:true</code>' %}
</div>


<div class="two-third-col">
  <h3>Wildcard search</h3>
  <p>To perform a single character wildcard search use <code>?</code>. Example: <code>entity:gene:P?2649</code>.</p>
  <p>To perform a multiple character wildcard search use <code>&ast;</code>. Example: <code>"Kepler-2*"</code>, <code>"Kepler-4*c"</code>.</p>
  <p>Tip: find all documents by just searching for <code>&ast;</code>.</p>
</div>
<div class="one-third-col">
</div>

<div class="two-third-col">
  <h3>filter:TODO</h3>
  <p>The special search <code>filter:TODO</code> lists the documents that the logged user still has to annotate or review, if any. See <a href="projects.html#task-distribution">Task Distribution</a> and <a href="collaboration.html#annotation-flows-task-distribution">Annotation Flows</a>.</p>
  <p>Note that you cannot search the TODO list for other users; the filter is only available for the currently logged in user.</p>
</div>
<div class="one-third-col">
</div>


<div class="two-third-col">
  <h3>Fuzzy search</h3>
  <p>Find similar terms (string based search) based on the Levenshtein Distance, or Edit Distance algorithm. Use <code>~</code> at the end of a single word term. Example: <code>roam~</code> will also find terms as <code>foam</code>.</p>
  <p>You can fine tune the <strong>similarity level</strong> by adding, at the end, a number between <code>0</code> (less similar) and <code>1</code> (more similar). Example: <code>roam~0.8</code>.</p>
</div>
<div class="one-third-col">
  {% include message.html message='The default similarity level is <code>0.5</code>.' %}
</div>


<div class="two-third-col">
  <h3>Proximity search</h3>
  <p>Finding words (string based search) within a specific distance away. Example: <code>"diabetes insulin"~10</code>, to search documents with the terms <code>diabetes</code> and <code>insulin</code> within 10 words of each other.</p>

</div>
<div class="one-third-col">

</div>


<div class="two-third-col">
  <h3>Boolean operators</h3>
  <p>Search queries can be combined using the operators <code>AND</code>, <code>OR</code>, <code>NOT</code> and <code>-</code>. Some examples:</p>
  <ul>
    <li><code>entity:GGP AND entity:Mutation</code> search for documents that contain <code>GGP</code> entities and <code>Mutation</code> entities.</li>
    <li><code>"type 1 diabetes" OR insulin</code> search for documents that contain "type 1 diabetes" or "insulin".</li>
    <li><code>"type 1 diabetes" NOT insulin</code> search for documents that contain "type 1 diabetes" but not "insulin". This operator cannot be used with just one term.</li>
    <li><code>-entity:GGP</code> search for documents that don't contain mentions of genes, i.e. <code>GGP</code> entities.</li>
  </ul>

</div>
<div class="one-third-col">
  {% include message.html message='Remember to use <strong>upper case</strong>: <code>AND</code>, <code>OR</code> and <code>NOT</code>.' %}
</div>

<div class="two-third-col">
  <h3>Escaping Special Characters</h3>
  <p>To escape these special characters use the <code>\</code> before the character. For example to search for <code>PD-L1</code> use the query: <code>PD\-L1</code>.</p>

</div>
<div class="one-third-col">
  {% include message.html message="The current list of <br/><strong>special characters</strong> are <code>+</code> <code>-</code> <code>!</code> <code>&quot;</code> <code>&amp;&amp;</code> <code>&verbar;&verbar;</code> <code>(</code> <code>)</code> <code>{</code> <code>}</code> <code>[</code> <code>]</code> <code>&Hat;</code> <code>~</code> <code>&ast;</code> <code>?</code> <code>:</code> <code>\</code>" %}
</div>

<div class="two-third-col">
  <h3>Experimental search query fields</h3>
  <p>These are currently valid for scientific articles.</p>
  <table style="width:100%">
    <tr>
      <th>Field</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>language</code></td>
      <td><code>language:fre</code></td>
      <td>Retrieve all documents written in the language specified</td>
    </tr>
    <tr>
      <td><code>orgs</code></td>
      <td><code>orgs:university of Finland</code></td>
      <td>Retrieve all documents, which were written by authors with affiliations related to the term specified</td>
    </tr>
    <tr>
      <td><code>authors_full</code></td>
      <td><code>authors_full:mueller</code></td>
      <td></td>
    </tr>
    <tr>
      <td><code>authors_key</code></td>
      <td><code>authors_key:"t goldberg"</code></td>
      <td></td>
    </tr>
    <tr>
      <td><code>publication</code></td>
      <td><code>publication:nature</code></td>
      <td>Retrieve all documents, which were written by the specified journal</td>
    </tr>
    <tr>
      <td><code>published</code></td>
      <td><code>published:2018</code> <code>published:2018-03-06</code> <code>published:[2013 to NOW]</code></td>
      <td>Retrieve all documents published in a specified time frame.</td>
    </tr>
  </table>
  <br/>
</div>
<div class="one-third-col">
</div>
