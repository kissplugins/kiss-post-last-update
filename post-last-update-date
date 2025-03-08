<?php
/**
 * Plugin Name:       KISS Post Last Updated Date
 * Plugin URI:        https://kissplugins.com
 * Description:       Provides shortcodes [kiss_last_updated] and [kiss-last-updated] to display the last updated date of the current post/page/CPT in Month Day, Year format.
 * Version:           1.1.0
 * Author:            KISS Plugins
 * Author URI:        https://kissplugins.com
 * License:           GPL2
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       kiss-post-last-updated-date
 */

/**
 * Security check: Exit if accessed directly.
 */
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Define plugin version constant.
 */
if ( ! defined( 'KISS_POST_LAST_UPDATED_VERSION' ) ) {
    define( 'KISS_POST_LAST_UPDATED_VERSION', '1.1.0' );
}

/**
 * Shortcode callback to display the last updated date of the current post.
 *
 * @return string
 */
function kiss_post_last_updated_date_shortcode() {
    global $post;

    if ( ! isset( $post->ID ) ) {
        return ''; // No post context available.
    }

    // Sanitize the ID just in case.
    $post_id = absint( $post->ID );

    // Retrieve the last modified date in the format "January 1, 2025"
    $last_updated_date = get_the_modified_date( 'F j, Y', $post_id );

    // Return the formatted date or an empty string if none.
    return $last_updated_date ? esc_html( $last_updated_date ) : '';
}

/**
 * Register the shortcodes.
 * Both [kiss_last_updated] and [kiss-last-updated] point to the same callback.
 */
function kiss_post_last_updated_date_register_shortcode() {
    add_shortcode( 'kiss_last_updated', 'kiss_post_last_updated_date_shortcode' );
    add_shortcode( 'kiss-last-updated', 'kiss_post_last_updated_date_shortcode' );
}
add_action( 'init', 'kiss_post_last_updated_date_register_shortcode' );

/**
 * Add settings link to plugin listing page.
 * This will link to a simple "status" page for convenience.
 *
 * @param array $links Existing plugin action links.
 * @return array
 */
function kiss_post_last_updated_date_action_links( $links ) {
    $settings_link = '<a href="admin.php?page=kiss-post-last-updated-date-status">'
                     . esc_html__( 'Plugin Status', 'kiss-post-last-updated-date' ) . '</a>';
    array_unshift( $links, $settings_link );
    return $links;
}
add_filter( 'plugin_action_links_' . plugin_basename( __FILE__ ), 'kiss_post_last_updated_date_action_links' );

/**
 * Register a simple admin page for plugin status.
 */
function kiss_post_last_updated_date_add_admin_menu() {
    add_menu_page(
        esc_html__( 'KISS Last Updated', 'kiss-post-last-updated-date' ),
        esc_html__( 'KISS Last Updated', 'kiss-post-last-updated-date' ),
        'manage_options',
        'kiss-post-last-updated-date-status',
        'kiss_post_last_updated_date_status_page'
    );
}
add_action( 'admin_menu', 'kiss_post_last_updated_date_add_admin_menu' );

/**
 * Content of the plugin's status page.
 */
function kiss_post_last_updated_date_status_page() {
    ?>
    <div class="wrap">
        <h1><?php esc_html_e( 'KISS Post Last Updated Date - Status', 'kiss-post-last-updated-date' ); ?></h1>
        <p><?php esc_html_e( 'Plugin Version:', 'kiss-post-last-updated-date' ); ?> <?php echo esc_html( KISS_POST_LAST_UPDATED_VERSION ); ?></p>
        <p>
            <?php
            esc_html_e( 'Shortcodes:', 'kiss-post-last-updated-date' );
            echo ' [kiss_last_updated], [kiss-last-updated] ';
            esc_html_e( 'Use either of these shortcodes to display the last updated date of the current post or page.', 'kiss-post-last-updated-date' );
            ?>
        </p>
    </div>
    <?php
}

/**
 * Changelog and Readme (for reference within the plugin file):
 *
 * = 1.1.0 =
 * * Added [kiss-last-updated] shortcode, retained [kiss_last_updated].
 * * Both shortcodes point to the same callback to display the last updated date.
 *
 * = 1.0.0 =
 * * Initial release.
 * * Shortcode [kiss_last_updated] to display the last updated date of the current post/page/CPT in Month Day, Year format.
 *
 * == Description ==
 * This plugin provides shortcodes [kiss_last_updated] and [kiss-last-updated] that can be placed
 * in any page, post, or CPT to display the date it was last updated in a user-friendly format.
 * Ideal for legal pages such as Terms of Use or Privacy Policy.
 *
 * == Usage ==
 * Place [kiss_last_updated] or [kiss-last-updated] anywhere in the content of a post, page, or CPT.
 * When viewed, it will display the last updated date in the format "Month day, year".
 */
