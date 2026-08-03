# Custom Sorting with Maps

A map is always sorted by key (ascending, by default). To sort differently,
you either (a) give the map a custom key-comparator, or (b) convert to a
vector of pairs and sort that.

## (a) Custom comparator for key order

    bool cmpDesc(int a, int b) {
        return a > b; // descending keys
    }

    map<int, int, bool(*)(int,int)> mp(cmpDesc);
    mp[3] = 10;
    mp[1] = 20;
    // iterates 3, 1 (descending)

## (b) Sort map by value (most common need)

Maps can't be sorted by value directly — convert to vector<pair> first.

    map<string,int> mp = {{"a",5}, {"b",2}, {"c",8}};

    vector<pair<string,int>> v(mp.begin(), mp.end());

    bool cmpByValue(pair<string,int> a, pair<string,int> b) {
        return a.second > b.second; // descending by value
    }

    sort(v.begin(), v.end(), cmpByValue);
