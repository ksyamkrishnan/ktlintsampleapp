When using addKtlintCheckGitPreCommitHook, my changed_files with broken rule still got successfully

Please find the pre-commit hook scripts generated:

#!/bin/sh
set -e
######## KTLINT-GRADLE HOOK START ########

CHANGED_FILES="$(git --no-pager diff --name-status --no-color --cached -- public/trunk/ | awk '$1 != "D" && $2 ~ /\.kts|\.kt/ { print $2}')"

if [ -z "$CHANGED_FILES" ]; then
    echo "No Kotlin staged files."
    exit 0
fi;

echo "Running ktlint over these files:"
echo "$CHANGED_FILES"

./public/trunk/gradlew -p ./public/trunk --quiet ktlintCheck -PinternalKtlintGitFilter="$CHANGED_FILES"

echo "Completed ktlint run."

echo "Completed ktlint hook."
######## KTLINT-GRADLE HOOK END ########
