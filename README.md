# Block-Editor-template-for-CPT


To define a **Block Editor template** for any **Custom Post Type (CPT)**, you follow the same method by:

1. **Modifying the `template` argument** within the `register_post_type()` function.
2. **Specifying the desired blocks** (like paragraph, button, image, etc.) that will automatically appear when creating a new post of that type.
3. **Using `template_lock` (optional)** to control whether users can add, remove, or rearrange blocks within the template.

### General Steps for Any CPT:
1. **Register the CPT** as usual.
2. Add a `template` argument to define which blocks will appear by default when adding a new post.
3. Customize the blocks as needed (e.g., placeholders, default values, class names).

### Example for Another CPT (e.g., "Project"):
If you had a custom post type called "Project" and you wanted to define a Block Editor template for it, the code would look similar to this:

```php
// Register Project CPT
function register_project_cpt() {
    $labels = array(
        'name'                  => _x( 'Projects', 'Post Type General Name', 'my-theme' ),
        'singular_name'         => _x( 'Project', 'Post Type Singular Name', 'my-theme' ),
        'menu_name'             => __( 'Projects', 'my-theme' ),
        'name_admin_bar'        => __( 'Project', 'my-theme' ),
        'add_new_item'          => __( 'Add New Project', 'my-theme' ),
        'new_item'              => __( 'New Project', 'my-theme' ),
        'edit_item'             => __( 'Edit Project', 'my-theme' ),
        'view_item'             => __( 'View Project', 'my-theme' ),
    );

    $args = array(
        'label'                 => __( 'Project', 'my-theme' ),
        'labels'                => $labels,
        'supports'              => array( 'title', 'editor', 'thumbnail' ), // Title, editor, and featured image support
        'public'                => true,
        'show_in_rest'          => true, // Enable Block Editor (Gutenberg)
        'has_archive'           => true,
        'rewrite'               => array( 'slug' => 'projects' ),
        'menu_icon'             => 'dashicons-portfolio', // Custom icon for Project CPT
        'template'              => array( // Define the block editor template
            array( 'core/heading', array(
                'level' => 2,
                'placeholder' => 'Project Title',
            )),
            array( 'core/paragraph', array(
                'placeholder' => 'Describe your project...',
            )),
            array( 'core/image', array(
                'align' => 'center',
                'className' => 'project-image',
            )),
            array( 'core/button', array(
                'text' => 'View Project',
                'url'  => '#', // Placeholder URL
                'className' => 'button-primary',
            )),
        ),
        'template_lock'         => 'all', // Optional: Locks the template, users can't remove blocks
    );

    register_post_type( 'project', $args );
}
add_action( 'init', 'register_project_cpt' );
```

### Customizing the Template:
- **Blocks**: You can add different types of blocks (e.g., heading, paragraph, image, button, etc.) depending on the structure you want.
- **Block Settings**: Each block can have its own settings, like a placeholder, default text, button URL, or custom CSS class.
- **Template Lock**: Set it to `'all'` to lock the template (users can't remove or move blocks), or `'insert'` to allow adding new blocks but prevent removing the default ones.

### Repeating the Process:
For each custom post type (CPT), you would:
- Use this same method.
- Adjust the `template` argument based on the specific block structure you want for that post type.

### Key Takeaways:
- You will follow the same approach to define a block editor template for each custom post type.
- The key difference lies in customizing the blocks (types and settings) according to the needs of each post type.
