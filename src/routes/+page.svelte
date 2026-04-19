<style>
h1, h2, h3 {
	color: #eee;
}
h1 {
	text-align: center;
}
h2 {
	background-color: #111;
	padding: 12px 24px;
	border-radius: 8px;
	text-align: center;
	max-width: 800px;
	margin: 8px auto;
}
p, li {
	color: #ddd;
}
h3, p, ol, ul {
	max-width: 800px;
	margin: auto;
	padding-top: 4px;
	padding-bottom: 4px;
	line-height: 1.5;
}
a {
	color: orange;
}
</style>

<h1>Code Review</h1>
<h2>Enhancement #1: 
	<a target=_blank href="https://youtu.be/pCuMqB6IoeE">YouTube</a>
</h2>
<h2>Enhancement #2: 
	<a target=_blank href="https://youtu.be/m-yL_wTFInE">YouTube</a>
</h2>
<h2>Enhancement #3: 
	<a target=_blank href="https://youtu.be/m4qKMkWKkLY">YouTube</a>
</h2>
<h1>Enhancement #1: Software Design and Engineering</h1>
<h2>Original: 
	<a target=_blank href="https://github.com/furthings/furthings.art/tree/4b806734e17b94af367fb0593343448c42e7ccb4">Github</a>
</h2>
<h2>Enhanced: 
	<a target=_blank href="https://github.com/furthings/furthings.art">Github</a>
</h2>
<h2>Narrative</h2>
<h3>Description</h3>
<p>
	I initially created this project in 2023 for a digital artist to act as the landing page for her clients. It is a static site that uses HTML, CSS, and JS. There are five main pages:
</p>
<ol>
	<li>index.html</li>
	<ul>
		<li>The home page which allows the user to navigate to any of the other pages.</li>
	</ul>
	<li>pricesheet.html</li>
	<ul>
		<li>A page detailing the prices of products that the client sells.</li>
	</ul>
	<li>autoquote.html</li>
	<ul>
		<li>A page that allows the user to calculate the price of a commission using the business logic laid out on the pricesheet page.</li>
	</ul>
	<li>tos.html</li>
	<ul>
		<li>A page about the client's business's terms of service.</li>
	</ul>
	<li>about.html</li>
	<ul>
		<li>A page about the client's business.</li>
	</ul>
</ol>
<h3>Justification of Inclusion</h3>
<p>
	I selected this artifact because it was written in an adhoc fashion as the artist gave me her design requirements. This led to a lot of code duplication, like repeated HTML blocks and JS functions. I enhanced the artifact by creating reusable Svelte components. Namely, a footer, price listing, and image viewer component. This way, the look of these elements can be maintained in one place, rather than having to constantly use the browser's debugger to find where in the HTML to make changes. This enhancement shows my ability to design modular logic in a front-end web context.
</p>
<h3>Reflection</h3>
<p>
	The biggest challenge I faced for this enhancement was having a singular function that loads the `prices.csv` file. This file is maintained by the client using one column for the listing name, and one for the price. My solution was creating a Typescript module that exposes a function which loads the data from the file by returning a promise using the Fetch API.
</p>
<p>
	Another challenge I faced was image loading. Files that are stored in the `/src/lib` directory have a different name once they're compiled using the Svelte-kit static adapter. In order to make the file retain its name, you have to put it in the `/src/static` directory. However, there is a node plugin that can automatically generate multiple versions of an image to give an optimal pixel density depending on the device - which cannot be used with static. In order to handle the changing of filenames, the images have to be loaded using the `import.meta.glob` function to store them in a map structure.
</p>
<p>
	Lastly, I made a point to make the type safety as strong as a could for the client's prices which took some time to nail down.
</p>
<h1>Enhancement #2: Algorithms and Data Structures</h1>
<h2>Original: 
	<a target=_blank href="https://github.com/natelwhite/CS330">Github</a>
</h2>
<h2>Enhanced: 
<a target=_blank href="https://github.com/natelwhite/Capstone-CS330">Github</a>
</h2>
<h2>Narrative</h2>
<h3>Description</h3>
<p>
	This artifact was originally created around 6 months ago for CS330, a course on computational graphics. The program renders a scene in real-time using blinn-phong shading with various textures.
</p>
<h3>Justification of Inclusion</h3>
<p>
	I selected this artifact because of its overall structure. During the course, we were given quite a bit of code. One class, `ShaderManager`, implemented all of the low-level logic associated with graphics programming: passing vertex and fragment uniforms, creating index/vertex/depth buffers, etcetera. Another class, `Meshes`, defined primitive vertex attributes. Of the logic that I authored, the bulk of it was the render function. We had to use primitive mesh objects (also given to us) in combination with the transformation values: translation, rotation, and scale, to place each primitive one by one in order to create more complex geometry. In my humble opinion, this project taught me little to nothing about graphics programming in general. Also, since the `ShaderManager` and `Meshes` code was distributed separate from the project, as it did not change throughout the course, I don't have access to those files anymore. Meaning, I can't compile the original program without reverse engineering these parts.
</p>
<p>
	Luckily, I've dabbled in graphics programming using <a href="https://github.com/libsdl-org/sdl">SDL</a>. A few months before taking this course, the SDL3 GPU API was released. Similar to OpenGL, it supports a variety of hardware including Vulkan, DirectX, and Metal. It can also handle window events, which GLFW was being used for. Lastly, <a href="https://github.com/spnda/fastgltf">fastgltf</a> can be used to load mesh data from a GLTF file. I believe my use of these libraries shows my ability to understand and implement algorithms (render function, data load, and data sort) that utilize a variety of data structures (maps, arrays, vectors, strings, etc.).
</p>
<h3>Reflection</h3>
<p>
	The biggest challenge I faced for this enhancement was storing vertex data in a buffer on the GPU. In my previous grahphics projects, I used multiple vertex buffers, one for each vertex attribute (position, normals, etc.). This time, I wanted to use a single vertex buffer with interleaved attributes.
</p>
<p>
	Another challenge I faced was memory safety. The original program used `delete` and `new` quite a few times. My enhancement uses smart pointers to avoid this and indicate memory ownership. Resources stored on the GPU however, cannot be used with smart pointers since the destructor function uses two parameters (i.e. <a href="https://wiki.libsdl.org/SDL3/SDL_ReleaseGPUGraphicsPipeline">SDL_ReleaseGPUGraphicsPipeline</a>). Instead of smart pointers, I created C++ templates that make the written code more consistent for allocating deallocating the memory: <a href="https://github.com/natelwhite/Capstone-CS330/blob/main/include/GPUResources.hpp">GPUResources</a>.
</p>
<p>
	Lastly, I've never dealt with material data aside from setting constants in the fragment shader. Meaning, I had to learn how to load, store, and use the material data in the GLTF file. I wasn't able to implement textures, but the albedo, roughness, and metallic values are properly passed to the fragment shader.
</p>
<h1>Enhancement #3: Databases</h1>
<h2>Original: 
<a target=_blank href="https://github.com/natelwhite/cs465-fullstack/tree/50e631f5b6276862689e2d4d5e0a2e0f7aa4b5bc">Github</a>
</h2>
<h2>Enhanced: 
<a target=_blank href="https://github.com/natelwhite/cs465-fullstack/tree/module7">Github</a>
</h2>
<h2>Narrative</h2>
<h3>Description</h3>
<p>
	This artifact was originally created around 4 months ago for CS465, a course on fullstack development. There are two programs, the Angular frontend, and the Express server which has a MongoDB database. All of the packages are managed by Node. All of these technologies put together creates the MEAN stack.
</p>
<h3>Justification of Inclusion</h3>
<p>
	I selected this artifact because it seemed very barebones. 8 weeks is not nearly enough time to create a complete fullstack application. However, it was a great way to show us how to do every thing required (create server endpoints, authenticate credentials, make database queries, etc.) without a bunch of complexity. I also have a small idea for a social media app designed for a specific community. With that in mind, I adjusted the app to allow so that a user may have a 'friendship' with another user.
</p>
<h3>Reflection</h3>
<p>
	This biggest challenge I faced for this enhancement was writing database queries. Most of my database experience was with relational databases. Since MongoDB isn't relational and therefore doesn't have foreign keys, cascading updates are not possible. I ended up creating a server endpoint for each database action: send friend request, accept friend request, reject friend request, and unfriend. These endpoints create two queries based on the value passed as an endpoint parameter and a field in the request body to update two users.
</p>
