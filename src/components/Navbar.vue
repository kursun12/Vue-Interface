<template>
		<nav>
        <ul>
            <li><a href="home.html">Home</a></li>
            <li><a href="blog.html">Blog</a></li>
            <li><a href="news.html">News</a></li>
            <li><a href="blog.html">Blog</a></li>
            <li><a href="news.html">News</a></li>
        </ul>
    </nav>
</template>

<script>

    export default {
        name: "Navbar"
        
    }
</script>

<style lang="css">

nav {
    background-color: #333;
    border: 1px solid #333;
    color: #fff;
    display: block;
    margin: 0;
    overflow: hidden;
}
nav ul{
    margin: 0;
    padding: 0;
    list-style: none;
}
nav ul li {
    margin: 0;
    display: inline-block;
    list-style-type: none;
    transition: all 0.2s;
}

nav > ul > li > a {
    color: #aaa;
    display: block;
    line-height: 2em;
    padding: 0.5em 2em;
    text-decoration: none;

}

nav li > ul{
    display : none;
    margin-top:1px;
    background-color: #bbb;

}

nav li > ul li{
    display: block;
}

nav  li > ul li a {
    color: #111;
    display: block;
    line-height: 2em;
    padding: 0.5em 2em;
    text-decoration: none;
}

nav li:hover {
    background-color: #666;
    text-decoration: #fff;
}
nav li:hover > ul{
    position:absolute;
    display : block;
}
nav li > ul > li ul  {
    display: none;
    background-color: #888;
}
nav li > ul > li:hover > ul  {
    position:absolute;
    display : block;
    margin-left:100%;
    margin-top:-3em;
}

a:hover 
{
     color:white!important; 
     text-decoration:none; 
     cursor:pointer;  
}
</style>