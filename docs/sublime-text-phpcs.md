### 安装phpcs(PHP_CodeSniffer)
### 配置示例
```
{
    // Plugin settings

    // Turn the debug output on/off
    "show_debug": true,
    "phpcs_execute_on_save": true,
    "phpcs_command_on_save": false,
    "phpmd_command_on_save": false,
    // Which file types (file extensions), do you want the plugin to
    // execute for
    "extensions_to_execute": ["php"],

    // Do we need to blacklist any sub extensions from extensions_to_execute
    // An example would be ["twig.php"]
    "extensions_to_blacklist": [],

    // PHP-CS-Fixer settings

    // Fix the issues on save
    "php_cs_fixer_on_save": true,

    // Show the quick panel
    "php_cs_fixer_show_quick_panel": false,

    // Path to where you have the php-cs-fixer installed
    "php_cs_fixer_executable_path": "~/.composer/vendor/bin/php-cs-fixer",

    // Additional arguments you can specify into the application
    "php_cs_fixer_additional_args": {
        "--rules": "@PSR1, @PSR2, @Symfony"
    },
}
```
