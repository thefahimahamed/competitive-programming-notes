# Custom Sorting Vector of Pairs

Sort a vector<pair<int,int>> using a custom comparator function instead of default (which sorts by first, then second).

## Using a comparator function

    bool cmp(pair<int,int> a, pair<int,int> b) {
        return a.second < b.second; // sort by second element ascending
    }

    sort(v.begin(), v.end(), cmp);

## Using a lambda (shorter)

    sort(v.begin(), v.end(), [](pair<int,int> a, pair<int,int> b) {
        return a.second > b.second; // descending by second
    });

## Comparator function variations

    bool cmpAsc(pair<int,int> a, pair<int,int> b) {
        return a.second < b.second; // ascending by second
    }

    bool cmpDesc(pair<int,int> a, pair<int,int> b) {
        return a.second > b.second; // descending by second
    }

    bool cmpTieBreak(pair<int,int> a, pair<int,int> b) {
        if (a.second != b.second) return a.second < b.second; // by second first
        return a.first < b.first; // if tie, by first
    }

    sort(v.begin(), v.end(), cmpAsc);
