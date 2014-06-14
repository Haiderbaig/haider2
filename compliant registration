<?php
/**
 * @package Registration
 */
/*
Plugin Name: Registration_system
Plugin URI: http://wordpress.org/
Description: Custom registration plugin 
Version: 1.0.0
Author: Automattic
Author URI: http://wordpress.org/
License: GPLv2 or later
*/


// Register a Complaints post type in wordpress

add_action( 'init', 'complaints_registration_init' );
/**
 * Register a book post type.
 *
 * @link http://codex.wordpress.org/Function_Reference/register_post_type
 */
function complaints_registration_init() {
	$labels = array(
		'name'               => _x( 'Complaints', 'Complaints', 'your-plugin-textdomain' ),
		'singular_name'      => _x( 'Complaint', 'Complaint', 'your-plugin-textdomain' ),
		'menu_name'          => _x( 'Complaints', 'admin menu', 'your-plugin-textdomain' ),
		'name_admin_bar'     => _x( 'Complaints', 'add new on admin bar', 'your-plugin-textdomain' ),
		'add_new'            => _x( 'Add New Complaint', 'book', 'your-plugin-textdomain' ),
		'add_new_item'       => __( 'Add New Complaint', 'your-plugin-textdomain' ),
		'new_item'           => __( 'New Complaint', 'your-plugin-textdomain' ),
		'edit_item'          => __( 'Edit Complaint', 'your-plugin-textdomain' ),
		'view_item'          => __( 'View Complaint', 'your-plugin-textdomain' ),
		'all_items'          => __( 'All Complaints', 'your-plugin-textdomain' ),
		'search_items'       => __( 'Search Complaints', 'your-plugin-textdomain' ),
		'parent_item_colon'  => __( 'Parent Complaint:', 'your-plugin-textdomain' ),
		'not_found'          => __( 'No Complaint found.', 'your-plugin-textdomain' ),
		'not_found_in_trash' => __( 'No Complaint found in Trash.', 'your-plugin-textdomain' )
	);

	$args = array(
		'labels'             => $labels,
		'public'             => true,
		'publicly_queryable' => true,
		'show_ui'            => true,
		'show_in_menu'       => true,
		'query_var'          => true,
		'rewrite'            => array( 'slug' => 'complaint' ),
		'capability_type'    => 'post',
		'has_archive'        => true,
		'hierarchical'       => false,
		'menu_position'      => null,
		'supports'           => array( 'title', 'editor', 'author', 'thumbnail', 'excerpt', 'comments' )
	);

	register_post_type( 'complaints', $args );
        flush_rewrite_rules();
}


// Create Register page on plugin activation
function myplugin_activate() {
    
    //ADD a new results page
    $post_id = -1;

        // Setup custom vars
        $author_id = 1;
        $slug = 'regsiter-a-complaint';
        $title = 'Register A Complaint';

        // Check if page exists, if not create it
        if ( null == get_page_by_title( $title )) {

            $uploader_page = array(
                    'comment_status'        => 'closed',
                    'ping_status'           => 'closed',
                    'post_author'           => $author_id,
                    'post_name'                     => $slug,
                    'post_title'            => $title,
                    'post_status'           => 'publish',
                    'post_type'                     => 'page'
            );

            $post_id = wp_insert_post( $uploader_page );


            if ( !$post_id ) {

                    wp_die( 'Error creating template page' );

            } else {

                    update_post_meta( $post_id, '_wp_page_template', 'register_page_template.php' );
                    //saving page ID that we just created for later usage!!.
                    update_option('registration_page_id',$post_id);

        }
        
            }
}
//run the call back function on plugin activation!
register_activation_hook( __FILE__, 'myplugin_activate' );



// Register Page template Redirection
//Template fallback
add_action("template_redirect", 'my_theme_redirect');

function my_theme_redirect() {
    global $wp;
    $plugindir = dirname( __FILE__ );
    //public_html/test/wp-content/plugins/registration/
$the_page_id = get_option('registration_page_id');
    if( is_page( $the_page_id ))
    {
       $return_template = $plugindir.'/themefiles/'.'register_page_template.php';
       do_theme_redirect($return_template);
    }
}

function do_theme_redirect($url) {
    global $post, $wp_query;
    if (have_posts()) {
        include($url);
        die();
    } else {
        $wp_query->is_404 = true;
    }
}

add_action("wp_head","complaintRegistraionStyle");

function complaintRegistraionStyle() {
    wp_register_style( 'complaint-registration-css', plugins_url( 'registration/themefiles/style.css' ) );
	wp_enqueue_style( 'complaint-registration-css' );
        
   // wp_register_script( 'validation-script-js', plugins_url( 'registration/themefiles/jqueryValidation.js' ),'jquery' );
	//wp_enqueue_script( 'validation-script-js' );
        
        // wp_register_script( 'custom-script-js', plugins_url( 'registration/themefiles/customJs.js' ),'jquery' );
	//wp_enqueue_script( 'custom-script-js' );
        
}



add_action('wp_ajax_remove-a-booking', 'submit_to_database');
add_action('wp_ajax_nopriv_remove-a-booking', 'submit_to_database');

function submit_to_database($title, $email, $description) {
   // Create post object
$my_post = array(
  'post_title'    => wp_strip_all_tags( $title ),
  'post_content'  => $description,
  'post_status'   => 'publish',
  'post_type'    => 'complaints'
);

// Insert the post into the database
$post_id = wp_insert_post( $my_post );
    return $post_id;
}

function complaintNumberEmail($email,$number){

$subject = "Your Complaint Number";
      
        $headers = 'From: Complaints Registration System <admin@localhost.com>' . "\r\n";
        // You have requested Password Reset for your account.
        $message = "Dear User Your complaint Number is ".$number;
        $message.= "---------------------------------------------\n";      
        wp_mail( $email, $subject, $message,$headers);

}

function complaints_func( $atts ){
	query_posts( 'post_type=complaints' );
echo '<ul>';
	// The Loop
while ( have_posts() ) : the_post(); ?>
    <a href="<?php the_permalink(); ?>"><li>
   <?php the_title(); ?>
    </li></a>
<?php
endwhile;
echo '</ul>';
// Reset Query
wp_reset_query();
	
}
add_shortcode( 'complaints', 'complaints_func' );
