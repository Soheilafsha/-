# -
Handler
const logger = Moralis.Cloud.getLogger();

Moralis.Cloud.afterDelete("Post", (request) => {
  const query = new Moralis.Query("Comment");
  query.equalTo("post", request.object);
  query
    .find()
    .then(Moralis.Object.destroyAll)
    .catch((error) => {
      logger.error(
        "Error finding related comments " + error.code + ": " + error.message
      );
    });
});
