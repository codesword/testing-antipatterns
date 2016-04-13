```ruby
describe RepoActivator, "#deactivate" do
  let(:repo) {
    create(:repo)
  }

  let(:activator) {
    allow(RemoveHoundFromRepo).to receive(:run)
    allow(AddHoundToRepo).to receive(:run).and_return(true)

    RepoActivator.new(github_token: "githubtoken", repo: repo)
  }

  let!(:github_api) {
    hook = double(:hook, id: 1)
    api = double(:github_api, remove_hook: true)
    allow(api).to receive(:create_hook).and_yield(hook)
    allow(GithubApi).to receive(:new).and_return(api)
    api
  }

  context "when repo deactivation succeeds" do
    it "marks repo as deactivated" do
      activator.deactivate

      expect(repo.reload).not_to be_active
    end

    it "removes GitHub hook" do
      activator.deactivate

      expect(github_api).to have_received(:remove_hook)
      expect(repo.hook_id).to be_nil
    end

    it "returns true" do
      expect(activator.deactivate).to be true
    end
  end
end
```

A better approach

```ruby
describe RepoActivator, "#deactivate" do
  context "when repo deactivation succeeds" do
    it "marks repo as deactivated" do
      repo = create(:repo)
      activator = build_activator(repo: repo)
      stub_github_api

      activator.deactivate

      expect(repo.reload).not_to be_active
    end

    it "removes GitHub hook" do
      repo = create(:repo)
      activator = build_activator(repo: repo)
      github_api = stub_github_api

      activator.deactivate

      expect(github_api).to have_received(:remove_hook)
      expect(repo.hook_id).to be_nil
    end

    it "returns true" do
      activator = build_activator
      stub_github_api

      result = activator.deactivate

      expect(result).to be true
    end
  end

  def build_activator(token: "githubtoken", repo: build(:repo))
    allow(RemoveHoundFromRepo).to receive(:run)
    allow(AddHoundToRepo).to receive(:run).and_return(true)

    RepoActivator.new(github_token: token, repo: repo)
  end

  def stub_github_api
    hook = double(:hook, id: 1)
    api = double(:github_api, remove_hook: true)
    allow(api).to receive(:create_hook).and_yield(hook)
    allow(GithubApi).to receive(:new).and_return(api)
    api
  end
end
```
