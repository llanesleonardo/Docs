Back: [Pull Requests](./pullrequest.md)

# Filtering and searching issues and pull requests

To find detailed information about a repository on GitHub, you can filter, sort, and search issues and pull requests that are relevant to the repository.

## Filtering issues and pull requests

---

Issues and pull requests come with a set of default filters you can apply to organize your listings.

You can find a pull request where you or a team you're a member of is requested for review with the search qualifier review-requested:[USERNAME] or team-review-requested:[TEAMNAME].

You can filter issues and pull requests to find:

- All open issues and pull requests
- Issues and pull requests that you've created
- Issues and pull requests that are assigned to you
- Issues and pull requests where you're @mentioned

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues or Pull requests.
3. Above the list, select the Filters dropdown menu, then click the type of filter you're interested in.

## Filtering issues and pull requests by assignees

---

Once you've assigned an issue or pull request to someone, you can find items based on who's working on them.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues or Pull requests.
3. Above the list of issues or pull requests, select the Assignee dropdown menu.
4. The Assignee drop-down menu lists everyone who has write access to your repository. Click the name of the person whose assigned items you want to see, or click Assigned to nobody to see which issues are unassigned.

## Filtering issues and pull requests by labels

---

Once you've applied labels to an issue or pull request, you can find items based on their labels.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues or Pull requests.
3. Above the list of issues or pull requests, click Labels.
4. In the list of labels, click a label.

## Filtering pull requests by review status

---

You can use filters to list pull requests by review status and to find pull requests that you've reviewed or other people have asked you to review.

You can filter a repository's list of pull requests to find:

- Pull requests that haven't been reviewed yet
- Pull requests that require a review before they can be merged
- Pull requests that a reviewer has approved
- Pull requests in which a reviewer has asked for changes
- Pull requests that you have reviewed
- Pull requests that someone has asked you directly to review
- Pull requests that someone has asked you, or a team you're a member of, to review

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Pull requests.
3. In the upper-right corner, select the Reviews dropdown menu.
4. Choose a filter to find all of the pull requests with that filter's status.

## Using search to filter issues and pull requests

---

You can use advanced filters to search for issues and pull requests that meet specific criteria.

## Searching for issues and pull requests

---

The issues and pull requests search bar allows you to define your own custom filters and sort by a wide variety of criteria. You can find the search bar on each repository's Issues and Pull requests tabs and on your Issues and Pull requests dashboards.

### About search terms

---

With issue and pull request search terms, you can:

- Filter issues and pull requests by author: state:open type:issue author:octocat
- Filter issues and pull requests that involve, but don't necessarily @mention, certain people: state:open type:issue involves:octocat
- Filter issues and pull requests by assignee: state:open type:issue assignee:octocat
- Filter issues and pull requests by label: state:open type:issue label:"bug"
- Filter out search terms by using - before the term: state:open type:issue -author:octocat

For issues, you can also use search to:

- Filter for issues that are linked to a pull request by a closing reference: linked:pr
- Filter issues by the reason they were closed: is:closed reason:completed or is:closed reason:"not planned"

For pull requests, you can also use search to:

- Filter draft pull requests: is:draft
- Filter pull requests that haven't been reviewed yet: state:open type:pr review:none
- Filter pull requests that require a review before they can be merged: state:open type:pr review:required
- Filter pull requests that a reviewer has approved: state:open type:pr review:approved
- Filter pull requests in which a reviewer has asked for changes: state:open type:pr review:changes_requested
- Filter pull requests by reviewer: state:open type:pr reviewed-by:octocat
- Filter pull requests by the specific user requested for review: state:open type:pr review-requested:octocat
- Filter pull requests that someone has asked you directly to review: state:open type:pr user-review-requested:@me
- Filter pull requests by the team requested for review: state:open type:pr team-review-requested:github/docs
- Filter for pull requests that are linked to an issue that the pull request may close: linked:issue

## Sorting issues and pull requests

---

Filters can be sorted to provide better information during a specific time period.

You can sort any filtered view by:

- The newest created issues or pull requests
- The oldest created issues or pull requests
- The most commented issues or pull requests
- The least commented issues or pull requests
- The newest updated issues or pull requests
- The oldest updated issues or pull requests
- The most added reaction on issues or pull requests

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Issues or Pull requests.
3. Above the list of issues or pull requests, select the Sort dropdown menu, then click a sort method.

To clear your sort selection, click Sort > Newest.

## Sharing filters

---

When you filter or sort issues and pull requests, your browser's URL is automatically updated to match the new view.

You can send the URL that issues generates to any user, and they'll be able to see the same filter view that you see.

For example, if you filter on issues assigned to Hubot, and sort on the oldest open issues, your URL would update to something like the following:

```
/issues?q=state:open+type:issue+assignee:hubot+sort:created-asc
```
