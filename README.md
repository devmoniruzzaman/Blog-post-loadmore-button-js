document.addEventListener("DOMContentLoaded", function() {
    let visiblePosts = 3;
    const loadMoreBtn = document.querySelector('.load-more-btn');
    const blogPosts = document.querySelectorAll('.blog-area .et_pb_post');

    // Hide all posts except the first 3
    blogPosts.forEach((post, index) => {
        if (index >= visiblePosts) post.style.display = 'none';
    });

    // Load More functionality
    loadMoreBtn.addEventListener('click', function(event) {
        event.preventDefault(); // Prevent default anchor behavior

        const hiddenPosts = Array.from(blogPosts).filter(post => post.style.display === 'none');
        hiddenPosts.slice(0, 3).forEach(post => {
            post.style.display = 'block';
            post.style.opacity = 0;
            setTimeout(() => {
                post.style.transition = 'opacity 0.5s ease-in-out';
                post.style.opacity = 1;
            }, 50);
        });

        // Hide button when no more posts to load
        if (hiddenPosts.length <= 3) {
            loadMoreBtn.style.display = 'none';
        }
    });
});
