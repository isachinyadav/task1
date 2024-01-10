# task1
#!/bin/bash

# Define the command version
VERSION="v0.1.0"

# Define the manual page for the command
MANUAL="internsctl - Custom Linux Command

NAME
    internsctl - Custom Linux Command

SYNOPSIS
    internsctl [OPTION]...
    internsctl user create <username>
    internsctl user list [--sudo-only]
    internsctl file getinfo [OPTIONS] <file-name>

DESCRIPTION
    internsctl is a custom Linux command designed for specific operations.

OPTIONS
    --help      Display this help and exit.
    --version   Output version information and exit.

USER COMMANDS
    create <username>    Create a new user with the specified username.
    list [--sudo-only]   List all regular users or users with sudo permissions.

FILE COMMANDS
    getinfo [OPTIONS] <file-name>   Get information about a file.

OPTIONS FOR FILE COMMANDS
    --size, -s               Print the size of the specified file.
    --permissions, -p        Print file permissions.
    --owner, -o              Print file owner.
    --last-modified, -m      Print last modified time.

EXAMPLES
    internsctl user create john_doe
    internsctl user list
    internsctl user list --sudo-only
    internsctl file getinfo --size hello.txt
    internsctl file getinfo --permissions hello.txt
    internsctl file getinfo --owner hello.txt
    internsctl file getinfo --last-modified hello.txt

AUTHOR
    Your Name <your.email@example.com>

VERSION
    $VERSION
"

# Function to display help
display_help() {
    echo "$MANUAL"
}

# Function to create a new user
create_user() {
    if [ $# -ne 1 ]; then
        echo "Error: Missing username. Usage: internsctl user create <username>"
        exit 1
    fi

    username=$1
    # Add logic to create a new user here
    echo "Creating user: $username"
}

# Function to list users
list_users() {
    if [ "$1" == "--sudo-only" ]; then
        # Add logic to list users with sudo permissions
        echo "Listing users with sudo permissions"
    else
        # Add logic to list all regular users
        echo "Listing all regular users"
    fi
}

# Function to get file information
get_file_info() {
    if [ $# -lt 2 ]; then
        echo "Error: Missing file name. Usage: internsctl file getinfo [OPTIONS] <file-name>"
        exit 1
    fi

    file_name=${@: -1}
    options=${@:1:$#-1}

    # Add logic to get file information based on options
    echo "Getting information for file: $file_name with options: $options"
}

# Main script logic
case "$1" in
    --help)
        display_help
        ;;
    --version)
        echo "internsctl $VERSION"
        ;;
    user)
        shift
        case "$1" in
            create)
                shift
                create_user "$@"
                ;;
            list)
                shift
                list_users "$@"
                ;;
            *)
                echo "Error: Unrecognized user command. Use 'internsctl --help' for usage information."
                exit 1
                ;;
        esac
        ;;
    file)
        shift
        case "$1" in
            getinfo)
                shift
                get_file_info "$@"
                ;;
            *)
                echo "Error: Unrecognized file command. Use 'internsctl --help' for usage information."
                exit 1
                ;;
        esac
        ;;
    *)
        echo "Error: Unrecognized option. Use 'internsctl --help' for usage information."
        exit 1
        ;;
esac

