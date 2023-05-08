Download Link: https://assignmentchef.com/product/solved-web422-assignment-5
<br>
The main objective in this assignment is to make an incremental update to the solution that you created for your Assignment 4 (ie: the “Blog” app).  For this assignment, we will publish a back-end API to manage the blog posts in your existing MongoDB Atlas account as well as wire up our application to use a single service to manage the data.  We will also enable users to view more than a single blog post by clicking on it from the main “blog” page.  A sample solution is provided here: <a href="https://limitless-forest-06256.herokuapp.com/">https://limitless</a><a href="https://limitless-forest-06256.herokuapp.com/">–</a><a href="https://limitless-forest-06256.herokuapp.com/">forest</a><a href="https://limitless-forest-06256.herokuapp.com/">–</a><a href="https://limitless-forest-06256.herokuapp.com/">06256.herokuapp.com/</a>

<strong>NOTE</strong>: If you are unable to start this assignment because there was an issue with your Assignment 4, please email your professor for a fresh (working) copy.

Specification:

<h1>Step 1 – The Database</h1>

It’s time that we move our application data out of a .json file and onto MongoDB Atlas.  Fortunately, everyone should have a working database instance from back in Assignment 1.  For this step, we simply need to remove all unused databases, add a new “blog” database with a “posts” collection, and populate it with data.




<h2>Removing Unused Databases</h2>




Log in to your MongoDB Atlas account and locate your “sample_supplies” database.  It can be found by clicking the “collections” button for one of your clusters (if you have multiple):










Once you have located it, you should see a number of other databases, ie: “sample_airbnb”, “sample_analytics”, etc, etc.):










Since we will not be using any of these other “sample” datasets this semester, you can go ahead and drop them to save space.  This can be done by hovering over each database and clicking the “garbage can” icon:










NOTE: Be sure <strong><u>not</u></strong> to drop “sample_supplies” as this will wipe out your “sales” data and your earlier assignments will cease to function.




Once this is complete, you should be left with a single “sample_supplies” database in the list:










<h2>Adding the “blog” Database</h2>




We can now go ahead and add in our new “blog” database by clicking the “+ Create Database” button.  Go ahead and enter “blog” for the database name and “posts” for the collection name:










With this complete, we should now have two databases in our cluster: “blog” and “sample_supplies”.




<h2>Inserting Sample Posts</h2>




Next, to ensure that our database has some content to work with, we must manually insert the same collection of “posts” from assignment 4, however without the “_id” attributes.  To save you the trouble of manipulating the .json file yourself, we have provided a clean version here:




<a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blogData.json">https://ict.senecacollege.ca/~patrick.crawford/shared/winter</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blogData.json">–</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blogData.json">2020/web422/A5/blogData.json</a>




<strong>Note:</strong> Keep that page open in your browser for now, as we will have to select all the text and copy it into our new “posts” collection.




To initiate this process, first click on your “posts” collection.  You should see that it has no documents yet.  To insert documents manually, click on the “insert document” button towards the right edge of the screen:










This should spawn a modal window titled: “Insert to Collection”.




Before we can copy &amp; paste all of our blogData (from the link above), we first have to switch the “view”.  This can be achieved by toggling the button next to the text “VIEW” in the modal window.  This should change your view to look like this (enabling us to paste the full “blogData” array):










Finally, delete lines 4 – 8 in the text box (effectively removing the suggested document) and proceed to copy the full content of the blogData.json file (from above) and paste it in to the window beneath the comment










With this done, we can now click “insert” to add the data!




<h2>The Connection String</h2>




The connection string for this database should be identical to your previous connection string, except with one change:




The text “sample_supplies” should be replaced with “blog”, for example, if your connection string looks like the below example:




mongodb+srv://yourUserName:<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="f28b9d8780a2938181859d8096b2919e8781869780c2df">[email protected]</a>

3abc.mongodb.net/<strong><u>sample_supplies</u></strong>?retryWrites=true&amp;w=majority”




it should be changed to:




mongodb+srv://yourUserName:<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="364f594344665745454159445276555a43454253440605575455185b59585159525418585342">[email protected]</a>/<strong><u>blog</u></strong>?retryWrites=true&amp;w=majority” Be sure to copy this value, as we will need it in the next step: “Configuring / Publishing the Blog API”







<h1>Step 2: Configuring / Publishing the Blog API</h1>

For this next step, we must publish an API (similar to what was done in assignment 1).  However for this assignment, rather than creating the API from scratch we can use a pre-configured “blogAPI”.  You can download a copy of it here:




<a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blog-API.zip">https://ict.senecacollege.ca/~patrick.crawford/shared/winter</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blog-API.zip">–</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blog-API.zip">2020/web422/A5/blog</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blog-API.zip">–</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/winter-2020/web422/A5/blog-API.zip">API.zip</a>




Once you have downloaded and extracted the above file, open the folder in Visual Studio Code and execute the command “npm install” to fetch the dependencies.




Finally, before you can test the API locally, you must update line 1 of “server.js” to include your new MongoDB Connection String (obtained above) for the “blog” database, ie:

<strong> </strong>

mongodb+srv://yourUserName:<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="a4ddcbd1d6f4c5d7d7d3cbd6c0e4c7c8d1d7d0c1d69497c5c6c78ac9cbcac3cbc0c68acac1d0">[email protected]</a>/<strong><u>blog</u></strong>?retryWrites=true&amp;w=majority”

<strong> </strong>

Once you have saved the changes, start the server with the command “node server.js”.  With the server running, access the route:




<a href="http://localhost:8080/api/posts?page=1&amp;perPage=10">http://localhost:8080/api/posts?page=1&amp;perPage=10</a>




You should now see your data!




Please feel free to play around with the API at this point, you will find that you can access posts by id, as well as filter posts by category (ie: <a href="http://localhost:8080/api/posts?page=1&amp;perPage=10&amp;category=Adventure">http://localhost:8080/api/posts?page=1&amp;perPage=10&amp;category=Adventure</a><a href="http://localhost:8080/api/posts?page=1&amp;perPage=10&amp;category=Adventure">)</a>  or tag (ie: <a href="http://localhost:8080/api/posts?page=1&amp;perPage=10&amp;tag=lovedit">http://localhost:8080/api/posts?page=1&amp;perPage=10&amp;tag=lovedit</a><a href="http://localhost:8080/api/posts?page=1&amp;perPage=10&amp;tag=lovedit">)</a> .




<h2>Pushing to Heroku</h2>




Now that our API is correctly configured, please push it to Heroku and save the link, as we will be using it throughout this assignment.







<h1>Step 3: Adding a “PostService” to our App</h1>

Before we can start working on the Blog App for Assignment 5, we must first make a copy of our completed Assignment 4 App (once again: If you are unable to start this assignment because there was an issue with your Assignment 4, please email your professor for a fresh (working) copy).




Open the folder containing the copy of Assignment 4 (now Assignment 5) in Visual Studio code and execute the “ng” command in the terminal to create a service with the class <strong>PostService</strong> (defined in post.service.ts).




This service will be responsible for working with our blog API (now on Heroku) using the HttpClient.

Therefore, we must make a few updates to our existing code, ie:

<ul>

 <li>In <strong>ts</strong> remove the _id property (the data in MongoDB does not contain one)</li>

 <li>Import and add the “HttpClientModule” to the “imports” array in app.module.ts</li>

</ul>




With the above configuration complete, we can now implement the following functions within our PostService:




<strong>NOTE</strong>: Set a constant variable called “perPage” at the top of the file and set its value to 6.  This will be our maximum results “perPage”




<h2>getPosts(page, tag, category): Observable&lt;BlogPost[]&gt;</h2>




This method will use HttpClient to return all of the posts available in the blogAPI for a specific page using the path: /api/posts?page=<strong><em>page</em></strong>&amp;perPage=<strong><em>perPage</em></strong> where <strong><em>page</em></strong> is the first parameter to the function and <strong><em>perPage</em></strong> is the constant defined (above).




Additionally, if the “tag” parameter is not null / undefined, then add &amp;tag=<strong><em>tag </em></strong>to the path.




<strong>IMPORTANT NOTE: </strong>The API will not permit you to use “#” in the “tag” parameter, ie: “tag=#scary” will not function, but “tag=scary” will.  Therefore, never invoke this function with a tag value that includes “#”.




Finally, if the “category” parameter is not null /undefined, then add &amp;category=<strong><em>category</em></strong> to the path




<h2>getPostbyId(id): Observable&lt;BlogPost&gt;</h2>




This method will use HttpClient to return a single post available in the blogAPI for a specific page using the path: /api/posts/<strong><em>id</em></strong> where <strong><em>id</em></strong> is the single parameter to the function.




<h2>getCategories(): Observable&lt;any&gt;</h2>




This method will use HttpClient to return an array of “Categories” in the format: {cat: <strong><em>string</em></strong>, num:

<strong><em>number</em></strong>} using the path /api/categories (Note: You should recognize this format, as it was the one used in assignment 4 for the “CategoriesComponent” data.)

<h2>getTags: Observable&lt;string[]&gt;</h2>

This method will use HttpClient to return an array of “Tags” (represented as strings) using the path /api/tags.




<h1>Step 4: Refactoring the “Blog” view (BlogComponent)</h1>

With all of our PostService methods in place, we can now start refactoring our code to start using it.

The best place to start is with the “BlogComponent”, since this is the primary interface for interacting with the blog.

To begin, open up blog.component.ts and make the following updates:

<ul>

 <li>Remove the import line for the “blogData.json” file (we will no longer be requiring it)</li>

 <li>Import &amp; inject the “PostService” service</li>

 <li>Import &amp; inject the “ActivatedRoute” service</li>

 <li>Make sure that you do not initialize the “blogPosts” property to anything by default (we’ll be using our service instead)</li>

 <li>Add the following properties to the component</li>

 <li>page (type: number, initial value: 1)</li>

 <li>tag (type: string, initial value: null)</li>

 <li>category (type: string, initial value: null)</li>

 <li>querySub (type: any, [ no initial value])</li>

 <li>In the ngOnInit() function, add the following logic</li>

</ul>

this.querySub = this.route.queryParams.subscribe(params =&gt; {




if(params[‘tag’]){     this.tag = params[‘tag’];     this.category = null;

}else{

this.tag = null;

}




if(params[‘category’]){

this.category = params[‘category’];

this.tag = null;

}else{

this.category = null;

}




this.getPage(+params[‘page’] || 1);




});

<ul>

 <li>Add a new getPage(num) function with the following logic:</li>

 <li>Get all of the blog posts using the values of num, this.tag and this.category.</li>

 <li>If the length of the data coming back &gt; 0, set this.blogPosts with the data and this.page with num</li>

</ul>




<ul>

 <li>In the ngOnDestroy() function, add the following logic: if(this.querySub) this.querySub.unsubscribe();</li>

</ul>

<h1>Step 5: The PagingComponent</h1>

With our “blog” page now showing live data from our database, it’s time to develop a new component to help with our pagination tasks within the BlogComponent.  To begin, create a new component called “PagingComponent” with the following specification:




<ul>

 <li>The following HTML can be used as its starting template:</li>

</ul>




&lt;nav aria-label=”Page navigation”&gt;

&lt;ul class=”pagination pagination-template d-flex justify-content-center”&gt;

&lt;li class=”page-item”&gt;&lt;a class=”page-link”&gt; &lt;i class=”fa fa-angle-left”&gt;&lt;/i&gt;&lt;/a&gt;&lt;/li&gt;

&lt;li class=”page-item”&gt;&lt;a class=”page-link”&gt;1&lt;/a&gt;&lt;/li&gt;

&lt;li class=”page-item”&gt;&lt;a class=”page-link”&gt; &lt;i class=”fa fa-angle-right”&gt;&lt;/i&gt;&lt;/a&gt;&lt;/li&gt;     &lt;/ul&gt;

&lt;/nav&gt;

<ul>

 <li>This component will accept a single property “<strong>page</strong>” (type: number)</li>

 <li>It will emit (output) the event “<strong>newPage</strong>” which will contain the new page number obtained by clicking on one of the “left” or “right” “page-item” buttons (details below)</li>

 <li>If the first “page-item” button is clicked (ie: “&lt;” ) , execute the following logic (placed in a separate “callback” function):</li>

 <li>If the value of “<strong>page</strong>” is greater than 1 emit the “<strong>newPage</strong>” event with a value of “<strong>page</strong>” – 1</li>

 <li>If the last “page-item” button is clicked (ie: “&gt;” ) , execute the following logic (placed in a separate “callback” function):</li>

 <li>emit the “<strong>newPage</strong>” event with a value of “<strong>page</strong>” + 1</li>

</ul>




Once completed, the component must be placed beneath the &lt;app-post-card&gt;&lt;/app-post-card&gt; element in blog.component.html using the html:




<h2><strong>&lt;div class=”w-100″&gt;&lt;app-paging&gt;&lt;/app-paging&gt;&lt;/div&gt; </strong></h2>

<strong> </strong>

Note: Do not forget to provide &lt;app-paging&gt; with a “[page]” input parameter (set to the value of “page” in the blog component), as well as wire up the emitted “(newPage)” event to execute “getPage($event)” – declared above.




<h1>Step 6: The CategoriesComponent</h1>

Now that we’re working with live blog data, we must refactor our CategoriesComponent to use it as well.  Start with updating the class “CategoriesComponent” (categories.component.ts) according to the following specification:




<ul>

 <li>Remove the hardcoded data assigned to the “categories” array</li>

 <li>Import &amp; inject the “PostService” service</li>

 <li>In the ngOnInit() function, add logic to populate the “categories” array using the “PostService” getCategories() function.</li>

 <li>Update the categories.component.html <strong>template </strong>to use the following “routerLink” attribute (assuming that “cat” is the current “category”:</li>

 <li>[routerLink]=”[‘/blog’]” [queryParams]=”{ category: cat.cat }”</li>

</ul>




<h1>Step 7: The TagsComponent</h1>

We must refactor our TagsComponent to use our new service as well.  Start with updating the class “TagsComponent” (tags.component.ts) according to the following:

<ul>

 <li>Remove the hardcoded data assigned to the “tags” array</li>

 <li>Import &amp; inject the “PostService” service</li>

 <li>In the ngOnInit() function, add logic to populate the “tags” array using the “PostService” getTags() function.</li>

 <li>Update the tags.component.html <strong>template </strong>to use the following “routerLink” attribute (assuming that “tag” is the current “tag”. Note: we eliminate the leading “#” by using substring(1)):</li>

 <li>[routerLink]=”[‘/blog’]” [queryParams]=”{ tag: tag.substring(1) }”</li>

</ul>







<h1>Step 8: The LatestPostsComponent</h1>

Up until now our “LatestPostsComponent” has been relying on a “posts” property for its data.  However, now that we are using an external data source, we can refactor this component to fetch the data itself.  First begin by opening “latest-posts.component.ts” and making the following changes:




<ul>

 <li>Remove the @Input() decorator from “posts”</li>

 <li>Import &amp; inject the “PostService” service</li>

 <li>In the ngOnInit() function, add logic to populate the “posts” array using the “PostService” getPosts(1, null, null) function. However, make sure that you only grab the first 3 results.  This can be done by once again using the .slice(0,3) method on the returned array</li>

</ul>

Next, locate both instances of the &lt;app-latest-posts&gt; component (blog.component.html &amp; post.component.html), it should look something like:




<ul>

 <li>&lt;app-latest-posts [posts]=”blogPosts.slice(0,3)”&gt;&lt;/app-latest-posts&gt;.</li>

</ul>




We simply want to remove the [posts] property, therefore it should be changed to

<strong> </strong>

<h2>        •    <strong>&lt;app-latest-posts&gt;&lt;/app-latest-posts&gt;</strong></h2>




Finally, in the template (latest-posts.component.html), update the <strong>routerLink</strong> attribute to link to the correct “post”, ie: [routerLink]=”[‘/post’, post._id]”







<h1>Step 9: The PostCardComponent &amp; Routing Update</h1>

With our main “Blog” page in fairly good working order,  we must finally update our PostCardComponent so that we can click on a specific blog post from within the “Blog” page and access it directly.  The main task here is to open the template (post-card.component.html) and make the following key change:




<ul>

 <li>Both <strong>routerLink=”/post”</strong> properties within the template need to be changed to the below (assuming “post” is the current “post” object: <strong>[routerLink]=”[‘/post’, post._id]” </strong></li>

</ul>

<strong> </strong>

Lastly, for this route to function properly, we need to update our “app-routing.module.ts” file to ensure that “post” has an “id” route parameter, ie “<strong>post/:id</strong>“.







<h1>Step 10: The PostDataComponent</h1>

The last major component to update for this assignment is the “PostDataComponent”.  To begin, open the post-data.component.ts file and make the following changes:




<ul>

 <li>Add the following property to the component</li>

 <li>querySub (type: any, [ no initial value])</li>

 <li>Remove the @Input() decorator from the “post” property as well as update any instance of the component that uses the [post] property binding, ie:</li>

</ul>




&lt;app-post-data [post]=”blogPosts[0]”&gt;&lt;/app-post-data&gt;




Should be changed to:




<h2><strong>&lt;app-post-data&gt;&lt;/app-post-data&gt;</strong></h2>




<ul>

 <li>Next, Import &amp; inject the “PostService” service</li>

 <li>Import &amp; Inject the “ActivatedRoute” service</li>

 <li>In the ngOnInit() function, add the following logic assuming that “route” references the ActivatedRoute service (NOTE: be sure to fill in the “TODO” with your own code)</li>

</ul>




this.querySub = this.route.params.subscribe(params =&gt;{

//TODO: Get post by Id params[‘id’] and store the result in this.post

})




<ul>

 <li>In the ngOnDestroy() function, add the following logic:</li>

 <li>if(this.querySub) this.querySub.unsubscribe();</li>

</ul>




<ul>

 <li>Finally, open up the template (post-data.component.html) and locate the &lt;div class=”post-tags”&gt; element. Inside, you will find an empty “routerLink” that needs to be refactored to link to the “blog” page with the correct tag filter, ie:</li>

</ul>




<ul>

 <li>[routerLink]=”[‘/blog’]” [queryParams]=”{ tag: tag.substring(1) }”</li>

</ul>







<h1>Step 11: New FooterPostsComponent</h1>




We’re almost done with the major components for the Blog and Page views, however we are still showing static (unrelated) blog posts in the footer of our blog.  To fix this, let’s add a new component:

“FooterPostsComponent” (Note: this component is very closely related to our “LatestPostsComponent”, so we will actually be recycling the code from that class)




Once you have crated your “FooterPostsComponent”, open the “footer-posts.component.ts” file and replace the code within the class with exact copy of the code within your “LatestPostsComponent” class (this will include the “posts” property, the constructor, and the ngOnInit() function).




Note:  “BlogPost” and “PostService” will need to be imported once this is complete.




<h2>Updating the Template</h2>




The “static” template for this component exists near the bottom of your “footer.component.html” file.  You should see a &lt;div class=”latest-posts”&gt;…&lt;/div&gt;.  Delete this entire element.




Now, instead of rendering the full &lt;div class=”latest-posts”&gt; element in the footer.component.html file, we will use the new “FooterPostsComponent”, ie:




&lt;app-footer-posts&gt;&lt;/app-footer-posts&gt;




<h2>Using “posts” in the Template (footer-posts.component.html)</h2>




For this template, you can use the following HTML for a single post (Note: You will have to repeat each &lt;div class=”post” for each “post”)




&lt;div class=”latest-posts”&gt;

&lt;div class=”post”&gt;

&lt;a routerLink&gt;

&lt;div class=”post d-flex align-items-center”&gt;

&lt;div class=”image”&gt;&lt;img src=”featuredImage” alt=”…” class=”img-fluid”&gt;&lt;/div&gt;

&lt;div class=”title”&gt;&lt;strong&gt;title&lt;/strong&gt;&lt;span class=”date last-meta”&gt;postDate&lt;/span&gt;&lt;/div&gt;

&lt;/div&gt;

&lt;/a&gt;

&lt;/div&gt;

&lt;/div&gt;







<ul>

 <li>The “routerLink” attribute should be changed to link to the correct post (using post._id)</li>

 <li>The &lt;img&gt; should use the “featuredImage” for the post</li>

 <li>The “title” should be the “title” for the post</li>

 <li>The “postDate should be the “postDate” for the post</li>

</ul>




<h1>Step 12: Angular “Date” Pipe</h1>

Finally, as a last step to clean our output, we will use Angular’s <a href="https://angular.io/api/common/DatePipe">date pipe</a> functionality.  The way this works is that whenever a date is rendered, ie {{post.postDate}}, you will pipe the output to date: “mediumDate”, ie: {{post.postDate}}  becomes <strong>{{post.postDate | date:’mediumDate’}} </strong>

<strong> </strong>

<strong>Note:  </strong>Do not forget to “pipe” the date for your post comments as well!




Extra Challenge!




When running our app, you might have noticed something slightly annoying from a usability perspective.  When we change routes, our scroll position on the page remains the same!  Ideally, we should be scrolled back to the top after every route change.  As an extra challenge, try researching this topic for yourself and implementing it within your application.