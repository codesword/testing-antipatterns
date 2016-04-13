```ruby
describe Event do
  describe "feedback form" do

    before do
      @user = create(:user, name: "ikem")
      @event = create(:event, title: "birthday")
    end

    context "before all activity" do
      it "is not displayed" do
        expect(@event).not_to include_feedback_form(@user)
      end
    end

    context "user posts a comment" do

      before { @event.create_comment(:user => @user) }

      it "is displayed" do
        expect(@event).to include_feedback_form(@user)
      end
    end

    context "user removes a comment" do

      before do
        comment = @event.create_comment(:user => @user)
        comment.destroy
      end

      it "is not displayed" do
        expect(@event).not_to include_feedback_form(@user)
      end
    end

    context "user posts a photo" do

      before { @user.post_photo(@event) }

      it "is displayed" do
        expect(@event).to include_feedback_form(@user)
      end
    end

    context "user likes it" do

      before { @user.like(@event) }

      it "is displayed" do
        expect(@event).to include_feedback_form(@user)
      end
    end
  end
end
```

A better approach.

```ruby
describe Event do
  describe "feedback form" do

    context "before all activity" do
      it "is not displayed" do
        user = create(:user)
        event = create(:event)
        expect(event).not_to include_feedback_form(user)
      end
    end

    context "user posts a comment" do

      it "is displayed" do
        event = create(:event)
        user = create(:user)
        event.create_comment(user: user)
        expect(event).to include_feedback_form(user)
      end
    end

    context "user removes a comment" do

      it "is not displayed" do
        user = create(:user)
        event = create(:event)
        comment = event.create_comment(user: user)
        comment.destroy
        expect(event).not_to include_feedback_form(user)
      end
    end

    context "user posts a photo" do
      it "is displayed" do
        user = create(:user)
        event = create(:event)
        user.post_photo(event)
        expect(event).to include_feedback_form(user)
      end
    end

    context "user likes it" do
      it "is displayed" do
        user = create(:user)
        event = create(:event)
        user.like(event)
        expect(event).to include_feedback_form(user)
      end
    end
  end
end
```
