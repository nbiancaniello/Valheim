### "copy_valheim_worlds" script

#!/bin/bash

SOURCE_DIR="/c/Users/nicol/AppData/LocalLow/IronGate/Valheim/worlds_local"
DEST_DIR="/c/Users/nicol/OneDrive/Desktop/Valheim Repo"

# Check if the source directory exists
if [ -d "$SOURCE_DIR" ]; then
    echo "Source directory found: $SOURCE_DIR"
else
    echo "Source directory does not exist. Exiting."
    exit 1
fi

# Check if the destination directory exists
if [ -d "$DEST_DIR" ]; then
    echo "Destination directory found: $DEST_DIR"
else
    echo "Destination directory does not exist. Exiting."
    exit 1
fi

# Copy the files from source to destination
echo "Copying files..."
cp -r "$SOURCE_DIR"/* "$DEST_DIR"

# Confirm the copy operation
echo "Files copied successfully to: $DEST_DIR"

### "push_valheim_worlds" script

#!/bin/bash

# Set the destination directory (your Valheim repo)
REPO_DIR="/c/Users/nicol/OneDrive/Desktop/Valheim Repo"

# Change to the repository directory
cd "$REPO_DIR" || { echo "Directory not found: $REPO_DIR"; exit 1; }

# Check if we're inside a Git repo
if [ ! -d ".git" ]; then
  echo "This is not a Git repository. Exiting."
  exit 1
fi

# Add all changes to staging (all files in the repo)
echo "Staging all changes..."
git add .

# Get the current timestamp for the commit message
TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S")

# Commit with the timestamp as the commit message
echo "Committing changes with message: 'Backup on $TIMESTAMP'"
git commit -m "Backup on $TIMESTAMP"

# Push the changes to the remote repository
echo "Pushing changes to remote repository..."
git push origin master

# Confirm that the push was successful
if [ $? -eq 0 ]; then
  echo "Changes pushed successfully!"
else
  echo "Failed to push changes."
  exit 1
fi
