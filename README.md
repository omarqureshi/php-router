WORK IN PROGRESS - DO NOT USE CURRENT README




# PHP router #

A simple router for PHP web applications to add RESTful routes with
shallow nesting of resources.

## Usage ##

### Simple usage ###

<pre><code>$r = new Router();
$r->resources("users");
</code></pre>

Generates the following routes:

<table>
<thead>
<tr>
<th>Method</th>
<th>Route</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr>
<td>GET</td>
<td>/users</td>
<td>index</td>
</tr>
<tr>
<td>GET</td>
<td>/users/:id</td>
<td>show</td>
</tr>
<tr>
<td>GET</td>
<td>/users/new</td>
<td>new</td>
</tr>
<tr>
<td>POST</td>
<td>/users</td>
<td>create</td>
</tr>
<tr>
<td>GET</td>
<td>/users/:id/edit</td>
<td>edit</td>
</tr>
<tr>
<td>PUT (as POST)</td>
<td>/users/:id</td>
<td>update</td>
</tr>
<tr>
<td>DELETE (as POST)</td>
<td>/users/:id</td>
<td>destroy</td>
</tr>
</tbody>
</table>

### Shallow nesting example ###

<pre><code>$r = new Router();
$r->resources("users")->resources("comments");
</code></pre>

This will not only match the above 7 routes, but the following 7 too:

<table>
<thead>
<tr>
<th>Method</th>
<th>Route</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr>
<td>GET</td>
<td>/users/:id/comments</td>
<td>index</td>
</tr>
<tr>
<td>GET</td>
<td>/comments/:id</td>
<td>show</td>
</tr>
<tr>
<td>GET</td>
<td>/users/:id/comments/new</td>
<td>new</td>
</tr>
<tr>
<td>POST</td>
<td>/users/:id/comments</td>
<td>create</td>
</tr>
<tr>
<td>GET</td>
<td>/comments/:id/edit</td>
<td>edit</td>
</tr>
<tr>
<td>PUT (as POST)</td>
<td>/comments/:id</td>
<td>update</td>
</tr>
<tr>
<td>DELETE (as POST)</td>
<td>/comments/:id</td>
<td>destroy</td>
</tr>
</tbody>
</table>


### Singular resource ###

As well as plural resources as described above, the router also
matches a singular resource:

<pre><code>$r = new Router();
$r->resource("cart")
</code></pre>

<table>
<thead>
<tr>
<th>Method</th>
<th>Route</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr>
<td>GET</td>
<td>/cart</td>
<td>show</td>
</tr>
<tr>
<td>GET</td>
<td>/cart/new</td>
<td>new</td>
</tr>
<tr>
<td>POST</td>
<td>/cart</td>
<td>create</td>
</tr>
<tr>
<td>GET</td>
<td>/cart/edit</td>
<td>edit</td>
</tr>
<tr>
<td>PUT (as POST)</td>
<td>/cart</td>
<td>update</td>
</tr>
<tr>
<td>DELETE (as POST)</td>
<td>/cart</td>
<td>destroy</td>
</tr>
</tbody>
</table>

### One off routes ###

You can also create one off routes - in the following manner

<pre><code>$r->map('/', array('controller' => 'home', 'action' => 'index'));</code></pre>

Using the string ':id' in your route lets you have a placeholder for
an alphanumeric id.
