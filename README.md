# flow-cytometry-galaxy-tools-setup

Galaxy tools setup for flow cytometry.

To produce lock files run and commit them to the same repo:

```
conda activate galaxy-bioblend
for tool_set in $( ls *.yaml ); do
	python scripts/fix-lockfile.py $tool_set
	python scripts/update-tool.py $tool_set
done

changes=$( git diff --exit-code | wc | awk '{ print $1 }' )
if [ "$changes" -gt 0 ]; then
	git add *.yaml.lock
	git commit -m "Update via $1"
else
	echo "Nothing to commit.."
fi
```

To install these tools to an instance:

```
conda activate galaxy-ephemeris
./scripts/install_tools.sh <GALAXY_URL> <GALAXY_ADMIN_API_KEY>
```
